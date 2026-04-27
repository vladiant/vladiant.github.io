---
layout: post
title: "C++ Core Guidelines Setup"
date: 2026-04-27    
tags: c++ development cmake ai
---

These flags complement the `.clang-tidy` configuration ( `cppcoreguidelines-*` : [Clang-Tidy Checks](https://clang.llvm.org/extra/clang-tidy/checks/list.html)) and apply to both GCC
and Clang unless otherwise noted. Flags are grouped by the guideline profile
they most directly support.

---

## Baseline (always enable)

```
-Wall -Wextra -Wpedantic
-Werror          # promote all warnings to errors once the codebase is clean
-std=c++17       # minimum standard recommended by the guidelines (c++20 preferred)
```

---

## Type Safety Profile
*Guidelines: Type.1 – Type.8*

```
# Forbid C-style casts; use static_cast/dynamic_cast/const_cast/reinterpret_cast
-Wold-style-cast

# Drop cv-qualifiers only deliberately
-Wcast-qual

# Warn on alignment-unsafe casts
-Wcast-align=strict          # GCC >= 8
-Wcast-align                 # earlier GCC / Clang

# Warn on reinterpret-cast-equivalent pointer conversions (Clang)
-Wundefined-reinterpret-cast # Clang

# Warn when a cast converts to a type with smaller range
-Wfloat-conversion
-Wdouble-promotion
-Wconversion
-Wsign-conversion
-Wsign-compare
-Wshorten-64-to-32           # Clang
-Warith-conversion           # GCC >= 10

# Varargs are banned (Type.8)
# (enforced by cppcoreguidelines-pro-type-vararg in clang-tidy)
```

---

## Bounds Safety Profile
*Guidelines: Bounds.1 – Bounds.4*

```
# Pointer arithmetic warnings
-Wpointer-arith

# Array-to-pointer decay
# (enforced by cppcoreguidelines-pro-bounds-array-to-pointer-decay in clang-tidy)

# Out-of-bounds detection at compile time
-Warray-bounds=2             # GCC; =2 enables more checks via value range
-Wstringop-overflow=4        # GCC >= 7
-Wstringop-overread          # GCC >= 11
-Wstringop-truncation        # GCC >= 8

# Zero-length and flexible array bounds
-Wzero-length-bounds         # GCC >= 10 (enabled by -Warray-bounds)
```

---

## Lifetime Safety Profile
*Guidelines: R.1 – R.11, I.11, F.42 – F.43*

```
# Use-after-move / dangling references
# (runtime: see Sanitizers section below)
-Wnull-dereference           # GCC >= 6, Clang
-Winit-self
-Wuninitialized
-Wmissing-field-initializers

# Strict aliasing enables the compiler to catch type-pun UB
-Wstrict-aliasing=3  -fstrict-aliasing

# Stack allocation limits (tune to your target)
-Wstack-usage=16384  -fstack-usage
-Walloca                     # GCC >= 7: flag alloca() use
-Wvla                        # warn on variable-length arrays (Clang -Wvla)
```

---

## Ownership / Resource Management
*Guidelines: R.10 – R.22, CP.20 – CP.26*

```
# Dynamic memory
# (enforced by cppcoreguidelines-no-malloc / cppcoreguidelines-owning-memory)

# Object slicing
# (enforced by cppcoreguidelines-slicing in clang-tidy)

# RAII: warn on unused [[nodiscard]] results
-Wunused-result              # implicit; explicit with [[nodiscard]]
```

---

## Expressions and Statements
*Guidelines: ES.1 – ES.87*

```
# Control flow clarity
-Wimplicit-fallthrough       # GCC >= 7, Clang: require [[fallthrough]] annotation
-Wswitch-enum                # all enum values must be handled or have a default
-Wswitch-default             # always require a default case

# Avoid uninitialised values
-Wconditional-uninitialized  # Clang: warns in conditional branches
-Wmaybe-uninitialized        # GCC

# Shadowing (ES.12)
-Wshadow

# Misleading formatting (ES.47)
-Wmisleading-indentation     # GCC >= 6, Clang

# Avoid goto (ES.76)
# (enforced by cppcoreguidelines-avoid-goto in clang-tidy)

# Integer overflow / shift (ES.103, ES.104)
-Wshift-overflow=2           # GCC >= 6
-Wshift-negative-value       # GCC >= 6
-Wsign-conversion

# Redundant / tautological expressions
-Wduplicated-cond            # GCC >= 6
-Wduplicated-branches        # GCC >= 7
-Wlogical-op                 # GCC: catch | used where || intended

# Floating-point
-Wfloat-equal                # ES.100
```

---

## Interfaces
*Guidelines: I.1 – I.27*

```
# Missing declarations (I.2: avoid non-const global variables)
-Wmissing-declarations
-Wmissing-variable-declarations  # Clang

# Non-null contract enforcement at compile time
-Wnonnull

# Format string safety (I.13)
-Wformat=2
-Wformat-security
-Wformat-nonliteral
-Wformat-signedness          # Clang >= 19, GCC
```

---

## Classes and Class Hierarchies
*Guidelines: C.1 – C.184*

```
# Rule of 0/5 (C.21, C.67)
# (enforced by cppcoreguidelines-special-member-functions in clang-tidy)

# Virtual function safety
-Wnon-virtual-dtor           # base class with virtual functions needs virtual dtor
-Woverloaded-virtual         # C.128

# Suggest final (C.139)
-Wsuggest-final-types        # GCC >= 5
-Wsuggest-final-methods      # GCC >= 5
-Wsuggest-override           # GCC >= 5; require 'override' keyword
```

---

## Functions
*Guidelines: F.1 – F.56*

```
# Keep functions small (F.4)
# (enforced by readability-function-size in clang-tidy)

# Always-inline / never-inline hints
-Winline

# Stack protection for unsafe functions
-Wstack-protector  -fstack-protector-strong
```

---

## Concurrency and Parallelism
*Guidelines: CP.1 – CP.111*

```
# Thread safety annotations (Clang)
-Wthread-safety
-Wthread-safety-analysis     # Clang: static analysis of mutex guards

# Data races (GCC, runtime)
# (use -fsanitize=thread at test time; see Sanitizers below)
```

---

## Error Handling
*Guidelines: E.1 – E.31*

```
# Exception-related
-Wterminate                  # GCC: warn when noexcept function may throw
-Wnoexcept                   # GCC: suggest noexcept

# Require handling of [[nodiscard]] return values
-Wunused-result
```

---

## Security / Hardening
*Guidelines: SL.str, I.13, F.4*

```
-Wwrite-strings              # string literals are const char[]
-Wformat-overflow=2          # GCC >= 7
-Wformat-truncation=2        # GCC >= 7

# Stack canary
-fstack-protector-strong

# Fortify glibc wrappers (catches unsafe buffer functions at compile time)
-D_FORTIFY_SOURCE=3

# Prevent UB from signed overflow being optimised away
-fno-strict-overflow         # or: -ftrapv to trap on signed overflow

# Control-flow integrity (Clang; link with -flto)
-fsanitize=cfi-icall
-fsanitize=cfi-vcall

# Unsafe-buffer-usage (Clang >= 19)
-Wunsafe-buffer-usage

# Bidirectional control characters in source (CVE-2021-42574)
-Wbidi-chars=any             # GCC >= 12, Clang
```

---

## Sanitizers (test / debug builds only – do NOT use in production)

```bash
# AddressSanitizer: detects heap/stack/global buffer overflows, use-after-free
-fsanitize=address -fno-omit-frame-pointer

# UndefinedBehaviorSanitizer: catches UB (signed overflow, misaligned access, etc.)
-fsanitize=undefined

# Combine both (most common test configuration):
-fsanitize=address,undefined -fno-omit-frame-pointer

# ThreadSanitizer: data race detection (cannot be combined with ASan)
-fsanitize=thread

# MemorySanitizer: uninitialised memory reads (Clang only)
-fsanitize=memory

# LeakSanitizer (included in ASan by default on Linux)
-fsanitize=leak
```

---

## CMake Integration

```cmake
# CMakeLists.txt snippet
add_compile_options(
    -Wall -Wextra -Wpedantic
    -Wold-style-cast -Wcast-qual -Wcast-align=strict
    -Wconversion -Wsign-conversion -Warith-conversion
    -Wshadow -Wnull-dereference -Wmisleading-indentation
    -Wduplicated-cond -Wduplicated-branches -Wlogical-op
    -Wimplicit-fallthrough -Wswitch-enum
    -Wshift-overflow=2 -Wshift-negative-value
    -Wformat=2 -Wformat-security
    -Wstrict-aliasing=3 -fstrict-aliasing
    -Wstack-protector -fstack-protector-strong
    -Wnon-virtual-dtor -Woverloaded-virtual
    -Wsuggest-final-types -Wsuggest-final-methods -Wsuggest-override
    -Wuninitialized -Wmaybe-uninitialized
    -Walloca -Wvla
    $<$<CONFIG:Debug>:-fsanitize=address,undefined>
    $<$<CONFIG:Debug>:-fno-omit-frame-pointer>
)

add_link_options(
    $<$<CONFIG:Debug>:-fsanitize=address,undefined>
)

# Enable clang-tidy
set(CMAKE_CXX_CLANG_TIDY clang-tidy;--config-file=${CMAKE_SOURCE_DIR}/.clang-tidy)
```

---

## References

* <https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines>
* <https://clang.llvm.org/extra/clang-tidy/checks/list.html>
* <https://clang.llvm.org/docs/analyzer/checkers.html>
* <https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html>
* <https://clang.llvm.org/docs/AddressSanitizer.html>
* <https://clang.llvm.org/docs/ThreadSanitizer.html>
* <https://github.com/isocpp/CppCoreGuidelines/blob/master/docs/Lifetime.pdf>
* <https://github.com/microsoft/GSL>

