---
layout: post
title: "GCC/Clang to MSVC Flag Mapping"
date: 2026-05-01    
tags: c++ development ai
---

These flags are selected to facilitate the <https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines>.

The MSVC compiler (`cl.exe`) uses a different flag syntax and warning model
than GCC/Clang. The table below maps the GCC/Clang flags from the
C++ Core Guidelines Setup post to their closest MSVC equivalents. Some flags have no direct counterpart;
in those cases the column notes the analogous mechanism (e.g. `/analyze`,
`/sdl`, or a specific `Cnnnn` warning enabled via `/wNNNN` or `/wdNNNN`).

---

## Flag Mapping Table

| GCC / Clang | MSVC | Notes |
|---|---|---|
| `-Wall` | `/W4` | MSVC `/Wall` is too noisy; `/W4` is the practical maximum. |
| `-Wextra` | `/W4` | Subsumed by `/W4`. |
| `-Wpedantic` | `/permissive-` | Strict standard conformance mode. |
| `-Werror` | `/WX` | Treat warnings as errors. |
| `-std=c++17` | `/std:c++17` | Use `/std:c++20` or `/std:c++latest` as needed. |
| `-Wold-style-cast` | `/w14640` (partial) | No exact match; clang-tidy `cppcoreguidelines-pro-type-cstyle-cast` recommended. |
| `-Wcast-qual` | `/w14302 /w14311` | Warn on cast that drops qualifiers / changes pointer size. |
| `-Wcast-align` | *(none)* | Use `/analyze` or clang-tidy. |
| `-Wconversion` | `/w14242 /w14254 /w14263` | Narrowing / signed-unsigned conversion warnings. |
| `-Wsign-conversion` | `/w14245 /w14365` | Signed/unsigned mismatch in conversion. |
| `-Wsign-compare` | `/w14389` | Signed/unsigned comparison. |
| `-Wshorten-64-to-32` | `/w14267` | Conversion from `size_t` to smaller type. |
| `-Wfloat-conversion` | `/w14244` | Conversion possible loss of data. |
| `-Wdouble-promotion` | *(none)* | No direct MSVC warning. |
| `-Wpointer-arith` | `/w14826` | Pointer arithmetic on `void*` etc. |
| `-Warray-bounds` | `/w16385 /w16386` (`/analyze`) | Static array bounds checks via SAL/`/analyze`. |
| `-Wstringop-overflow` | `/analyze` (C6385/C6386) | Buffer overrun analysis. |
| `-Wnull-dereference` | `/analyze` (C6011) | Null pointer dereference via static analysis. |
| `-Winit-self` | `/w14700` | Use of uninitialized local variable. |
| `-Wuninitialized` | `/w14700 /w26495` | C26495 from `/analyze` C++ Core Guidelines ruleset. |
| `-Wmaybe-uninitialized` | `/w14701 /w14703` | Potentially uninitialized variable. |
| `-Wmissing-field-initializers` | `/w15246` | Subobject initialization. |
| `-Wstrict-aliasing` / `-fstrict-aliasing` | *(default)* | MSVC always assumes strict aliasing. |
| `-Wstack-usage=N` | `/analyze:stacksize N` | Stack frame size analysis. |
| `-fstack-usage` | *(none)* | Use `/Gs` and `/analyze` reports. |
| `-Wvla` | `/wd4200` *(N/A)* | MSVC does not support C99 VLAs in C++. |
| `-Wunused-result` (`[[nodiscard]]`) | `/w14834` | Discarded `[[nodiscard]]` return value. |
| `-Wimplicit-fallthrough` | `/w15262` | Implicit switch fall-through. |
| `-Wswitch-enum` | `/w14062` | Enum value not handled in switch. |
| `-Wswitch-default` | `/w14065` | Switch with default but no case labels. |
| `-Wshadow` | `/w14456 /w14457 /w14458 /w14459` | Variable / parameter / member shadowing. |
| `-Wmisleading-indentation` | *(none)* | No direct MSVC warning. |
| `-Wshift-overflow` | `/w14146` | Shift count / overflow issues. |
| `-Wshift-negative-value` | `/w14146` | Same as above (negative shift). |
| `-Wduplicated-cond` | *(none)* | Use `/analyze` (C6235, C6237). |
| `-Wduplicated-branches` | *(none)* | Use `/analyze`. |
| `-Wlogical-op` | *(none)* | No direct MSVC warning. |
| `-Wfloat-equal` | *(none)* | No direct MSVC warning. |
| `-Wmissing-declarations` | `/w14505` | Unreferenced local function with internal linkage. |
| `-Wnonnull` | `/analyze` (C6387) | Argument may be null. |
| `-Wformat=2` / `-Wformat-security` | `/w14774 /w14777` | Format string mismatches. |
| `-Wnon-virtual-dtor` | `/w14265` | Class has virtual functions but non-virtual dtor. |
| `-Woverloaded-virtual` | `/w14263` | Member function does not override any base class virtual. |
| `-Wsuggest-override` | `/w26433` | C++ Core Guidelines: function should be marked `override`. |
| `-Wsuggest-final-types` / `-methods` | *(none)* | Use clang-tidy `cppcoreguidelines-virtual-class-destructor`. |
| `-Winline` | *(none)* | No direct MSVC warning. |
| `-fstack-protector-strong` | `/GS` | Buffer security check (enabled by default). |
| `-Wstack-protector` | *(none)* | `/GS` is on by default; no separate warning. |
| `-Wthread-safety` | *(none)* | No equivalent; use clang-tidy or `/analyze:plugin ConcurrencyCheck.dll`. |
| `-Wterminate` / `-Wnoexcept` | *(none)* | No direct MSVC warning. |
| `-Wwrite-strings` | `/Zc:strictStrings` | Enforce `const` for string literals. |
| `-Wformat-overflow` / `-Wformat-truncation` | `/analyze` (C6031, C6053) | Buffer / format truncation analysis. |
| `-D_FORTIFY_SOURCE=3` | `/sdl` | Security Development Lifecycle checks. |
| `-fno-strict-overflow` | *(default)* | MSVC does not optimize on signed overflow UB. |
| `-fsanitize=cfi-*` | `/guard:cf` | Control Flow Guard. |
| `-Wunsafe-buffer-usage` | `/analyze` (C26446, C26481-C26489) | C++ Core Guidelines bounds checks. |
| `-Wbidi-chars` | *(none)* | No direct MSVC warning. |
| `-fsanitize=address` | `/fsanitize=address` | AddressSanitizer (MSVC 16.9+). |
| `-fsanitize=undefined` | *(none)* | No UBSan in MSVC; use `/analyze` and `/RTCcsu` for some checks. |
| `-fsanitize=thread` | *(none)* | No TSan in MSVC. |
| `-fsanitize=memory` | *(none)* | No MSan in MSVC. |
| *(C++ Core Guidelines static analysis)* | `/analyze:plugin EspXEngine.dll` with `CppCoreCheck` ruleset | Native C++ Core Guidelines checker. |

> Tip: Enable `/analyze` with the **C++ Core Guidelines** ruleset
> (`CppCoreCheckRules.ruleset`) to obtain MSVC-side coverage closest to the
> GCC/Clang warning set. The `Cnnnn` warning numbers in the table can be tuned
> individually with `/wNNNN` (enable as warning) or `/wdNNNN` (disable).

---

## References

* <https://learn.microsoft.com/en-us/cpp/build/reference/compiler-options-listed-by-category>
* <https://learn.microsoft.com/en-us/cpp/code-quality/using-the-cpp-core-guidelines-checkers>
* <https://learn.microsoft.com/en-us/cpp/build/reference/analyze-code-analysis>
* <https://learn.microsoft.com/en-us/cpp/sanitizers/asan>
