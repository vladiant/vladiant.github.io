---
layout: post
title: "Modern CMake"
date: 2025-02-01
tags: cmake development make 
---

## Useful commands
* `cmake -B <build tree> -S <source tree>`
* `cmake --build <build tree>`

## Makefile generator
* `-G <generator name>`
* make
* ninja

## Force re-config and re-gen
* `--fresh`

## Useful options
* `--system-information`
* `--log-level=...`
* `--log-context`
* `--trace`

## Debug build system
* `--verbose`, `-v`
* `CMAKE_VERBOSE_MAKEFILE:BOOL=ON`

### Build targets:
* `cmake --build <build dir> --target exe_name --target lib_name`

### Clean target:
* `cmake --build <build dir> -t clean`
* `cmake --build <build dir> --clean-first`

## Install project
* `cmake --install <build tree>`
* `cmake --install <build tree> --install-prefix <prefix>`

## References
* [San Diego C++ Meetup #66 - Modern CMake and C++!](https://www.youtube.com/watch?v=lnUALZe7FhI)
* [Integrating C++ Code Generation Into a Large CMake Build - CB Bailey - ACCU 2024](https://www.youtube.com/watch?v=bCuH4cHPJ78)
* [cmake](https://cmake.org/cmake/help/latest/manual/cmake.1.html)
* [CMAKE_VERBOSE_MAKEFILE](https://cmake.org/cmake/help/latest/variable/CMAKE_VERBOSE_MAKEFILE.html)
* [cmake-configure-log](https://cmake.org/cmake/help/latest/manual/cmake-configure-log.7.html)
* <https://github.com/onqtam/awesome-cmake>
* <https://github.com/ema-mil/cpp-modern-template>
* <https://github.com/stfufane/aoc-cpp-template>