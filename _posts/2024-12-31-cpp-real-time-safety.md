---
layout: post
title: "C++ Real Time Safety"
date: 2024-12-32
tags: c++ design development peformance
---

## Real-time programming

### Worst case execution time must be
* Deterministic
* Known in advance
* Independent of input data
* Shorter than given deadline

### Nondeterministic execution time
* system calls
* allocations
* mutex locks/unlocks
* thrown exceptions
* indefinite calls (CAS loops, infinite loops)

## Existing strategies
* Shared experience -> takes time
* Code review -> prone to human error
* Profilers and debuggers -> manual process
* static_assert -> limited
* Documentation -> goes out of date

### Tool would
* assess real-time safety
* detect a wide range of violations
* point to problematic code
* Able to fail a CI pipeline

## RealtimeSanitizer
* `-fsanitize=realtime`
* <https://github.com/realtime-sanitizer/rtsan>

## Performance constraints
* [Performance Constraint Attributes](https://clang.llvm.org/docs/AttributeReference.html#performance-constraint-attributes)
* `[[clang::*]]`

### Attributes
* nonblocking
* blocking
* nonallocating
* allocating

### Compilation flags
* `-Wfunction-effects`
* `-Wperf-constraint-implies-noexcept`

## Comparing and contrasting

### RTSAN blind spots
* No guarantee of processor time
* No guarantee your code runs faster than allotted time
* No detection of hand-written assembly system calls
* Not all libc wrapper functions implemented
* No detection of nondeterministic loops

### Blind spots of Constraints
* No guarantee of processor time
* No guarantee your code runs faster than allotted time
* Misdeclared functions

## References
* [LLVM's Realtime Safety Revolution: Tools for Modern Mission Critical Systems - CppCon 2024](https://www.youtube.com/watch?v=KvhgNdxX6Uw)
* [RealtimeSanitizer](https://clang.llvm.org/docs/RealtimeSanitizer.html)
* [Attributes in Clang](https://clang.llvm.org/docs/AttributeReference.html)
* [Function Effect Analysis](https://clang.llvm.org/docs/FunctionEffectAnalysis.html)