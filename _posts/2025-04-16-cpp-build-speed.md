---
layout: post
title: "C++ Build Speed"
date: 2025-04-16
tags: c++ performance design
---

## Recommendation for includes
* Refactor massive header files
* Forward declarations
* Include what you use

## Templates recommendation
* Consider whether you need to use template metaprogramming (constexpr, consteval)
* Re-evaluate your API


## Why do modules help?
* Eliminate redundant parsing
* Precompiled headers ~ Modules

## Translation unit recommendations
* Precompiled headers
* Modules

## Dependency Management
* Builds should be purely functional
* Avoid large dependency bottlenecks
* Prefer smaller targets
* Explicitly expressed dependencies enables efficient hardware utilization while maintaining build correctness

## Tools
* <https://github.com/aras-p/ClangBuildAnalyzer>
* <https://github.com/nico/ninjatracing>
* [Perfetto](https://ui.perfetto.dev/)
* <https://github.com/google/perfetto>

## Takeaways
* Profile your builds
* Compilation requires parsing which isn't free
* Better hardware won't always save us from ourselves
* We are all stewards of our build times

## Reference
* [Why Is My C++ Build So Slow? Compilation Profiling and Visualization - Samuel Privett - CppCon 2024](https://www.youtube.com/watch?v=Oih3K-3eZ4Y)
* [Code examples](https://github.com/maspe36/WhyIsMyBuildSoSlow)
* [Clang -ftime-trace](https://clang.llvm.org/docs/analyzer/developer-docs/PerformanceInvestigation.html)
