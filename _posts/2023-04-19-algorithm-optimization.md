---
layout: post
title: "Algorithm Optimization"
date: 2023-04-19
tags: c++ performance
---

## Valgrind Setup
```bash
valgrind 
   --main-stacksize=180777216
   --tool=callgrind
   --cache-sim=yes
   --branch-sim=yes
   --dump-instr=yes
   --collect-jumps=yes
```

* Check miss rate

## Guidelines

* Use benchmarks and profiling tools
* Measure, measure and measure!

### Data
* Avoid using pointers in types
* Use as much of the cache line as possible (Data Oriented Design vs Object Oriented Design)
* Make data access predictable
* Watch out for false sharing in multithreaded systems
* Cache-oblivious algorithm
* Cache friendly containers (contigious memory) - [std::vector](https://en.cppreference.com/w/cpp/header/vector), [flat_set](https://en.cppreference.com/w/cpp/header/flat_set), [flat_map](https://en.cppreference.com/w/cpp/header/flat_map)

### Code
* Fit working set in cache
* Make "fast paths" branch-free sequences
* Inline catiously
   + Reduces branching
   + Facilitates code-reducing optimizations
   - Code duplication reduces effective cache size
* Take advantage of PGO (Profile Guided Optimization) and WPO (Whole Program Optimization)

## Reference
* [C++ Algorithmic Complexity, Data Locality, Parallelism, Compiler Optimizations, & Some Concurrency - Avi Lachmish - CppCon 2022](https://www.youtube.com/watch?v=0iXRRCnurvo)
* [Callgrind: a call-graph generating cache and branch prediction profiler](https://valgrind.org/docs/manual/cl-manual.html)
