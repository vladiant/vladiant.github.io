---
layout: post
title: "Useful C++ compiler flags (GCC and Clang) - 2"
date: 2026-04-14
tags: c++ performance test
---

# C++ Compiler Warning Flags

## Main
* -Wall
* -Wextra
* -Wpedantic
* -Wuninitialized
* -Wmissing-include-dirs
* -Wshadow
* -Wundef
* -Winvalid-pch

## Extra

### Control flow
* -Winit-self
* -Wswitch-enum  -Wswitch-default
* -Wformat=2  -Wformat-nonliteral  -Wformat-security  -Wformat-y2k

### Arithmetics
* -Wdouble-promotion
* -Wfloat-equal
* -Wpointer-arith

### Cast and conversion
* -Wstrict-overflow=5
* -Wcast-qual
* -Wcast-align
* -Wconversion
* -Wpacked

### Sanitizing
* -Wstrict-aliasing  -fstrict-aliasing
* -Wredundant-decls
* -Wmissing-declarations
* -Wmissing-field-initializers

### Security
* -Wwrite-strings
* -Wstack-protector  -fstack-protector
* -Wpadded
* -Winline
* -Wdisabled-optimization

### C specific
* -Waggregate-return
* -Wbad-function-cast
* -Wc++-compat

### C++ specific
* -Wzero-as-null-pointer-constant
* -Wctor-dtor-privacy
* -Wold-style-cast
* -Woverloaded-virtual

### GNU specific
* -Wlogical-op
* -Wstack-usage=1024  -fstack-usage  # -Wframe-larger-than=1024
* -Wtrampolines
* -Wvector-operation-performance

### GNU C++ specific
* -Wuseless-cast
* -Wnoexcept
* -Wstrict-null-sentinel

## GNU >= 5.0.0
* -Wsuggest-final-types
* -Wsuggest-final-methods
* -Wsuggest-override

## GNU >= 6.0.0
* -Wmisleading-indentation
* -Wshift-overflow
* -Wshift-negative-value
* -Wnull-dereference
* -Wshift-overflow=2
* -Wduplicated-cond

## C++ GNU >= 6.0.0
* Detect virtual inheritance: -Wvirtual-inheritance
* Detect templates: -Wtemplates
* Detect multiple inheritance: -Wmultiple-inheritance

## GNU >= 7.0.0
* -Wimplicit-fallthrough
* -Wunused-macros
* -Wformat-overflow=2
* -Wformat-truncation=2
* -Wstringop-overflow=4
* -Wduplicated-branches
* -Walloc-zero
* -Walloca

## GNU >= 8.0.0
* -Wcast-align=strict
* -Wstringop-truncation
* -Wextra-semi

## GNU >= 9.0.0
* -Wmultistatement-macros
* -Waddress-of-packed-member  # enabled by default

### C++ GNU >= 9.0.0
* -Wpessimizing-move  # implied by -Wall
* -Wredundant-move  # implied by -Wextra
* -Wdeprecated-copy  # implied by -Wextra
* -Wdeprecated-copy-dtor  # stricter: also warns when dtor is user-provided

## GNU >= 10.0.0
* -Warith-conversion
* -Wstring-compare  # implied by -Wextra

### C++ GNU >= 10.0.0
* -Wmismatched-tags  # off by default; eases porting to MSVC
* -Wredundant-tags  # off by default; warns about redundant class-key/enum-key

## GNU >= 11.0.0
* -Wmismatched-dealloc  # enabled by default
* -Wsizeof-array-div  # implied by -Wall
* -Wstringop-overread  # enabled by default

### C++ GNU >= 11.0.0
* -Wrange-loop-construct  # implied by -Wall
* -Wmismatched-new-delete  # implied by -Wall
* -Wvexing-parse  # enabled by default
* -Wctad-maybe-unsupported  # off by default; warns on CTAD without deduction guides
* -Wdeprecated-enum-enum-conversion  # default in C++20
* -Wdeprecated-enum-float-conversion  # default in C++20

## GNU >= 12.0.0
* -Wbidi-chars  # default: =unpaired; warns about misleading bidirectional control chars
* -Warray-compare  # warns about comparison between two array-typed operands

## GNU >= 13.0.0
* -Wxor-used-as-pow  # warns when ^ is likely meant as exponentiation

### C++ GNU >= 13.0.0
* -Wself-move  # warns on std::move of a value to itself
* -Wdangling-reference  # warns on references bound to temporaries whose lifetime ended

## GNU >= 14.0.0
* -Walloc-size  # warns about allocator-like functions with suspicious size arguments
* -Wcalloc-transposed-args  # warns if calloc num/size arguments appear transposed

### C++ GNU >= 14.0.0
* -Wnrvo  # warns when named return value optimization is prevented
* -Welaborated-enum-base  # warns about redundant enum-base in elaborated-type-specifier

## GNU >= 15.0.0
* -Wheader-guard  # implied by -Wall; warns about inconsistent header guard macros
* -Wleading-whitespace=spaces  # warns about indentation style violations
* -Wtrailing-whitespace=spaces  # warns about trailing whitespace

### C++ GNU >= 15.0.0
* -Wdefaulted-function-deleted  # warns when an explicitly defaulted function becomes deleted

## Clang specific

### Main
* -Werror=option-ignored
* -Warc-repeated-use-of-weak
* -Wbitfield-enum-conversion
* -Wc++11-compat-pedantic
* -Wclass-varargs
* -Wconditional-uninitialized
* -Wthread-safety

### Mistakes
* -Wconsumed
* -Wdirect-ivar-access
* -Wdisabled-macro-expansion
* -Wembedded-directive
* -Wexit-time-destructors
* -Wexpansion-to-defined
* -Wformat-pedantic
* -Widiomatic-parentheses
* -Winconsistent-missing-destructor-override
* -Winfinite-recursion
* -Wlocal-type-template-args
* -Wloop-analysis
* -Wmethod-signatures
* -Wmismatched-tags
* -Wmissing-braces
* -Wmissing-prototypes
* -Wmissing-variable-declarations
* -Wmost
* -Wmove
* -Wnonportable-system-include-path
* -Wnull-pointer-arithmetic
* -Wover-aligned
* -Woverriding-method-mismatch
* -Wpch-date-time
* -Wpragmas
* -Wreserved-id-macro
* -Wreserved-user-defined-literal
* -Wretained-language-linkage
* -Wsemicolon-before-method-body
* -Wsometimes-uninitialized
* -Wstring-conversion
* -Wsuper-class-method-mismatch
* -Wtautological-compare
* -Wundefined-reinterpret-cast
* -Wunreachable-code
* -Wunreachable-code-break
* -Wunreachable-code-loop-increment
* -Wunreachable-code-return
* -Wvector-conversion

### Sanitizing
* -Wcomma
* -Wduplicate-enum
* -Wduplicate-method-arg
* -Wduplicate-method-match
* -Wdynamic-exception-spec
* -Wempty-translation-unit
* -Wexplicit-ownership-type
* -Wignored-qualifiers
* -Wimplicit
* -Wkeyword-macro
* -Wnewline-eof
* -Wredundant-parens
* -Wstatic-in-inline
* -Wstrict-prototypes
* -Wweak-template-vtables
* -Wweak-vtables
* -Wzero-length-array

### Arrays
* -Warray-bounds-pointer-arithmetic
* -Wextended-offsetof
* -Wflexible-array-extensions

### Arithmetics
* -Wfloat-conversion
* -Wfloat-overflow-conversion
* -Wfloat-zero-conversion
* -Wshorten-64-to-32
* -Wsign-compare
* -Wsign-conversion

### Advices
* -Wcomment
* -Wdocumentation
* -Wdocumentation-pedantic
* -Wglobal-constructors
* -Wgnu
* -Wheader-hygiene
* -Wunneeded-internal-declaration
* -Wunneeded-member-function
* -Wvla
* -Wsuggest-final-types
* -Wsuggest-final-methods
* -Wsuggest-override
* -Wshift-overflow
* -Wshift-negative-value
* -Wnull-dereference
* -Wunused-macros

## Clang >= 6.0.0
* -Wextra-semi

## Clang >= 7.0.0
* -Wc++98-compat-extra-semi  # separated from -Wc++98-compat-pedantic

## Clang >= 10.0.0
* -Wimplicit-int-float-conversion  # warns on implicit float-to-int narrowing

## Clang >= 11.0.0
* -Wpointer-to-int-cast  # C: warns on cast of pointer to integer too small to hold all values
* -Wuninitialized-const-reference  # grouped under -Wuninitialized
* -Wimplicit-const-int-float-conversion  # grouped under -Wimplicit-int-float-conversion

## Clang >= 12.0.0
* -Wdeprecated-volatile  # C++20: warns on deprecated uses of volatile
* -Wnon-c-typedef-for-linkage  # warns on C-style typedef used to give linkage to unnamed type

## Clang >= 13.0.0
* -Wreserved-identifier  # warns about identifiers reserved by the C/C++ standard

## Clang >= 14.0.0
* -Wcast-function-type-strict  # stricter version of -Wcast-function-type
* -Wbitfield-constant-conversion  # warns on constant conversion in bitfield initializer

## Clang >= 16.0.0
* -Wfuture-compat  # warns about constructs that will be errors in future standards
* -Wsingle-bit-bitfield-constant-conversion  # separated from -Wbitfield-constant-conversion

## Clang >= 17.0.0
* -Wdeprecated-this-capture  # C++20: warns on deprecated capture of this with default =

## Clang >= 18.0.0
* -Wmissing-designated-field-initializers  # sub-group of -Wmissing-field-initializers
* -Wc++23-compat  # helps migrating code to C++23
* -Wc++2c-compat  # helps migrating code to C++26

## Clang >= 19.0.0
* -Wformat-signedness  # warns when format requires unsigned but signed arg is passed (and vice versa)
* -Wpre-c11-compat  # warns about C11 keywords used in pre-C11 language modes
* -Wtentative-definition-array  # warns when a tentative array definition is assumed to have one element
* -Wunsafe-buffer-usage  # warns about unsafe pointer/array operations (hardening)

## References
* <https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html>
* <https://gcc.gnu.org/onlinedocs/gcc/C-Dialect-Options.html>
* <https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html>
* <https://clang.llvm.org/docs/DiagnosticsReference.html>
* <https://gcc.gnu.org/gcc-9/changes.html>
* <https://gcc.gnu.org/gcc-10/changes.html>
* <https://gcc.gnu.org/gcc-11/changes.html>
* <https://gcc.gnu.org/gcc-12/changes.html>
* <https://gcc.gnu.org/gcc-13/changes.html>
* <https://gcc.gnu.org/gcc-14/changes.html>
* <https://gcc.gnu.org/gcc-15/changes.html>
