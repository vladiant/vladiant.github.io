---
layout: post
title: "Useful C++ compiler flags (GCC and Clang)"
date: 2021-08-14
tags: c++ performance test
---

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
* -Wunused-macros
* -Wstringop-overflow=4
* -Wduplicated-branches
* -Walloc-zero
* -Walloca

## GNU >= 8.0.0
* -Wcast-align=strict
* -Wstringop-truncation
* -Wextra-semi

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
  
## References
* <https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html>
* <https://gcc.gnu.org/onlinedocs/gcc/C-Dialect-Options.html>
* <https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html>
* <https://clang.llvm.org/docs/DiagnosticsReference.html>
