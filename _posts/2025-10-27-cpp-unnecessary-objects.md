---
layout: post
title: "C++ Unnecessary Objects"
date: 2025-10-27
tags: c++ performance coding development
---

## Recommendations

### Compiler warnings
* [-Wexit-time-destructors](https://clang.llvm.org/docs/DiagnosticsReference.html#wexit-time-destructors) (Clang)
* [-Wglobal-constructors](https://clang.llvm.org/docs/DiagnosticsReference.html#wglobal-constructors) (Clang)
* [-Wpessimizing-move](https://clang.llvm.org/docs/DiagnosticsReference.html#wpessimizing-move)
* [-Wrange-loop-construct](https://clang.llvm.org/docs/DiagnosticsReference.html#wrange-loop-construct)

### Clang-tidy checks
* [performance-unnecessary-value-param](https://clang.llvm.org/extra/clang-tidy/checks/performance/unnecessary-value-param.html)
* [performance-unnecessary-copy-initialization](https://clang.llvm.org/extra/clang-tidy/checks/performance/unnecessary-copy-initialization.html)
* [performance-for-range-copy](https://clang.llvm.org/extra/clang-tidy/checks/performance/for-range-copy.html)
* [modernize-pass-by-value](https://clang.llvm.org/extra/clang-tidy/checks/modernize/pass-by-value.html)
* [performance-inefficient-vector-operation](https://clang.llvm.org/extra/clang-tidy/checks/performance/inefficient-vector-operation.html)
* [performance-noexcept-move-constructor](https://clang.llvm.org/extra/clang-tidy/checks/performance/noexcept-move-constructor.html)
* [modernize-use-emplace](https://clang.llvm.org/extra/clang-tidy/checks/modernize/use-emplace.html)


### Key points
* In-place construction without copies or moves
* Pass non-trivial objects by reference
* Use view types ( [std::string_view](https://en.cppreference.com/w/cpp/string/basic_string_view.html) , [std::span](https://en.cppreference.com/w/cpp/container/span.html) )
* Use in-place constructors for STL types
* Use emplace
* Use transparent comparators for std::string in associative containers
* Move data to compile time
* Use clang-tidy checks and warnings

## Reference
* [C++ Performance Tips - Cutting Down on Unnecessary Objects - Prithvi Okade & Kathleen Baker](https://www.youtube.com/watch?v=ypkAKB9-2Is)
* [GCC Warning Options](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html)
* [Diagnostic flags in Clang](https://clang.llvm.org/docs/DiagnosticsReference.html)
* [Clang-Tidy Checks](https://clang.llvm.org/extra/clang-tidy/checks/list.html)
