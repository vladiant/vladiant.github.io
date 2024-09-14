---
layout: post
title: "Reduce Compilation Times C++"
date: 2024-09-15
tags: c++ development performance
---

## Build system
* `cmake -G Ninja`

## Linkers
* `lld` much faster than the default linker `ld` or `gold`
* `-fuse-ld=lld`
* `mold` is even faster than `lld`

## Compiler Caching
* `CCache`
* `ln -s ccache /usr/local/bin/g++`

## Open Source Tooling
* clang `-ftime-trace` flag creates a flame chart JSON file of each translation unit
* Open tracing output with `chrome://tracing`
* `ClangBuildAnalyzer` parses and summarizes these files
* GCC `-ftime-report` makes the compiler print some statistics to stderr about the time consumed by each pass when it finishes.

## Techniques
* Forward Declarations - `<iosfwd>`, dedicated headers with forward declarations
* Removing unused includes - `https://include-what-you-use.org/`, Graphviz
* Splitting Protocol and Implementation - Fundamental Theorem of Software Engineering, PIMPL
* Object Libraries
* Precompiled Headers - since CMake 3.16, headers that are often included bu not changed often, use profiling to determine headers to pre-compile
* Unity Build - since CMake 3.16

## Main Takeaways
* Profile your build to determine where to focus your effort
* Forward declarations
* Remove unused includes
* Split Protocol from Implementation
* Merge executables
* Tune precompiled headers
* Unity build and reducing number of files

## References
* [Reducing C++ Compilation Times Through Good Design - Andrew Pearcy - ACCU 2024](https://www.youtube.com/watch?v=ItcGevumW-8)
* [Ninja Build system](https://ninja-build.org/)
* [LLD - The LLVM Linker](https://lld.llvm.org/)
* [Gold Linker](https://en.wikipedia.org/wiki/Gold_(linker))
* [ld linker](https://linux.die.net/man/1/ld)
* [mold linker](https://github.com/rui314/mold)
* [Ccache — a fast C/C++ compiler cache](https://ccache.dev/)
* [time-trace: timeline / flame chart profiler for Clang](https://aras-p.info/blog/2019/01/16/time-trace-timeline-flame-chart-profiler-for-Clang/)
* [Clang command line argument reference](https://clang.llvm.org/docs/ClangCommandLineReference.html)
* <https://github.com/aras-p/ClangBuildAnalyzer>
* [GCC Developer Options](https://gcc.gnu.org/onlinedocs/gcc/Developer-Options.html)
* [Google C++ Style Guide : Forward Declarations](https://google.github.io/styleguide/cppguide.html#Forward_Declarations)
* <https://include-what-you-use.org/>
* [Graphviz](https://graphviz.org/)
* [CMake CMakeGraphVizOptions](https://cmake.org/cmake/help/latest/module/CMakeGraphVizOptions.html)
* [Fundamental Theorem of Software Engineering](https://en.wikipedia.org/wiki/Fundamental_theorem_of_software_engineering)
* [PIMPL](https://en.cppreference.com/w/cpp/language/pimpl)
* [CMake target_precompile_headers](https://cmake.org/cmake/help/latest/command/target_precompile_headers.html)
* [CMake UNITY_BUILD](https://cmake.org/cmake/help/latest/prop_tgt/UNITY_BUILD.html)
