---
layout: post
title: "Making Most Out of Compiler"
date: 2022-07-19
tags: c++ development performance
---

## Points
* Don't blame compilers for being slow. They will note generate the best possible code for you.
* There is a chance your code will grow a lot and you won't notice
* More visibility to your compiler opens more optimizations.
* Use `-O0 -g` for debugging purposes, use `-O3` for optimization purposes.
* Compilers assume really old hardware (e.g. core2 for x86, 2006), use better options.
* `-march=native` is extremely dangerous because of illegal instructions and non-homogeneous hardware

## LTO
* Link time optimizations
* Thin LTO provides summaries of modules
* `-flto , -flto=thin (LLVM)`
* Use thin LTO for release builds, usual without

## Faster than O0
* `-O1`
* `-fno-omit-frame-pointer`
* `-fno-optimize-sibling-calls`
* `-Og` -> for GCC only

## X86 Westmere era (2010)
* `-msse2, -msse3, -mssse3, -msse4.1, -msse4.1`
* `-mpclmul`
* `-maes`
* `-mcx16`
* `-mpopcnt`

## X86 Haswell era (2013)
* `-mavx, -mavx2`
* `-mbmi2`
* `-mfma`

## Why not avx/avx2/avx512 by default?
* Share AVX with non AVX -> CPU downclocking
* Heavy AVX (floating point) -> CPU downclocking

## Inline threshold for LLVM
* `-mllvm -inline-threshold=N` (default 225)
* Inclininig increases your build size and compile time.
* Idea: run `-mllvm -inline-threshold=1000` , compare benchmarks, set always_inline attributes to a dozen of calls


## Reference
* [Making the Most Out of Your Compiler - Danila Kutenin - CppCon 2021](https://www.youtube.com/watch?v=tckHl8M3VXM)
* [LLVM Vectorizing debug](https://llvm.org/docs/Vectorizers.html)
* [GCC Options That Control Optimization](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html)
* [ThinLTO](https://clang.llvm.org/docs/ThinLTO.html)
* [GCC x86 Options](https://gcc.gnu.org/onlinedocs/gcc/x86-Options.html)
