---
layout: post
title: "CMake C++20 Modules"
date: 2022-09-24
tags: cmake make c++20
---

## Working module branch of CMake
* <https://gitlab.kitware.com/ben.boeckel/cmake/>
* <https://gitlab.kitware.com/ben.boeckel/cmake/-/tree/cpp-modules-checkpoint>

## GCC - patch for named modules
* <https://github.com/mathstuf/gcc/tree/p1689r4>

## Snippet
```
cmake_minimum_required(VERSION 3.23)
project(simple CXX)
set(CMAKE_CXX_STANDARD 20)
add_library(simple)

target_sources(simple
   PRIVATE
   FILE_SET cxx_modules TYPE CXX_MODULES FILES
   A.cpp B.cpp
)
```

## References
* [CMake 2022 C++ Modules and More - Bill Hoffman - CppNow 2022](https://www.youtube.com/watch?v=hkefPcWySzI)
* [Mastering CMake](https://gitlab.kitware.com/cmake/mastering-cmake)
* [CMake Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
* [cmake-buildsystem(7)](https://cmake.org/cmake/help/latest/manual/cmake-buildsystem.7.html)
