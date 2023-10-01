---
layout: post
title: "CMake Case Studies"
date: 2023-09-19
tags: cmake make c++20 c++
---

## General
* Use latest CMake
* Find dependecies - [find_package](https://cmake.org/cmake/help/latest/command/find_package.html). Be careful with [add_subdirectory](https://cmake.org/cmake/help/latest/command/add_subdirectory.html) and [FetchContent](https://cmake.org/cmake/help/latest/module/FetchContent.html)
* Prepare for `FetchContent` users - manually namespace targets, make possible to disable packaging rules.
* Do not GLOB for sources.
* GenerateExportHeader - works for single library type.
* Put in `CMakeLists.txt` exactly what is necessary to produce a working build.
* Portability can lead to combinatorial explosion. Consider [cmake presets](https://cmake.org/cmake/help/latest/manual/cmake-presets.7.html)

## Create build targets
* [add_executable](https://cmake.org/cmake/help/latest/command/add_executable.html) - create an executable target
* [add_library](https://cmake.org/cmake/help/latest/command/add_library.html) - create a library target

## Working with targets
* [target_sources](https://cmake.org/cmake/help/latest/command/target_sources.html) - add source files to target
* [target_include_directories](https://cmake.org/cmake/help/latest/command/target_include_directories.html) - add include directories to target
* [target_compile_options](https://cmake.org/cmake/help/latest/command/target_compile_options.html) - add compile options to target
* [target_link_libraries](https://cmake.org/cmake/help/latest/command/target_link_libraries.html) - add libraries or linker flags to target
* `PRIVATE`, `PUBLIC`, `INTERFACE`

## Additional target properties
* [target_compile_definitions](https://cmake.org/cmake/help/latest/command/target_compile_definitions.html)
* [target_compile_features](https://cmake.org/cmake/help/latest/command/target_compile_features.html)
* [target_link_directories](https://cmake.org/cmake/help/latest/command/target_link_directories.html)
* [target_link_options](https://cmake.org/cmake/help/latest/command/target_link_options.html)
* [target_precompile_headers](https://cmake.org/cmake/help/latest/command/target_precompile_headers.html)

## Work with properties
* [get_target_property](https://cmake.org/cmake/help/latest/command/get_target_property.html)
* [set_target_properties](https://cmake.org/cmake/help/latest/command/set_target_properties.html)
* [function](https://cmake.org/cmake/help/latest/command/function.html)
* [cmake_parse_arguments](https://cmake.org/cmake/help/latest/command/cmake_parse_arguments.html)
* [generator-expressions](https://cmake.org/cmake/help/latest/manual/cmake-generator-expressions.7.html)
* [add_custom_command](https://cmake.org/cmake/help/latest/command/add_custom_command.html)

## Working with variables
* Set a normal variable
* Setting a cache entry

## Module File
* `CMAKE_MODULE_PATH`
* `FindOracle.cmake` file
* Environment variable used
* <https://github.com/SOCI/soci/blob/master/cmake/modules/FindOracle.cmake>
* [find_path](https://cmake.org/cmake/help/latest/command/find_path.html) - include path. Store result in `Oracle_INCLUDE_DIR`. [mark_as_advanced](https://cmake.org/cmake/help/latest/command/mark_as_advanced.html) to hide it from GUIs
* [find_library](https://cmake.org/cmake/help/latest/command/find_library.html) . Store result in `Oracle_LIBRARY`
* [find_program](https://cmake.org/cmake/help/latest/command/find_program.html) to find client programs.
* [execute_process](https://cmake.org/cmake/help/latest/command/execute_process.html) to call external program i.e. get the version.
* Check received variables using [FindPackageHandleStandardArgs](https://cmake.org/cmake/help/latest/module/FindPackageHandleStandardArgs.html)
* Create target `Oracle::Oracle`
```
if (NOT TARGET Oracle::Oracle)
   add_library(Oracle::Oracle UNKNOWN IMPORTED)
   set_target_properties(Oracle::Oracle PROPERTIES
      IMPORTED_LOCATION "{Oracle_LIBRARIES}"
      INTERFACE_INCLUDE_DIRECTORIES "{Oracle_INCLUDE_DIRS}")
endif()
```
* Add default include directories


## C++20 modules
* [import CMake; C++20 Modules](https://www.kitware.com/import-cmake-c20-modules)
* [Using CMake with C++20 modules](https://github.com/Kitware/CMake/blob/master/Help/dev/experimental.rst)
* [Online Example](https://godbolt.org/z/84hrMa6fz)

* [Static checks with CMake/CDash - iwyu, clang-tidy, lwyu, cpplint and cppcheck](https://www.kitware.com/static-checks-with-cmake-cdash-iwyu-clang-tidy-lwyu-cpplint-and-cppcheck/)

## References
* [import CMake: // 2023 State of C++20 modules in CMake - Bill Hoffman - CppNow 2023](https://www.youtube.com/watch?v=c563KgO-uf4)
* [The Challenges of Implementing C++ Header Units: C++ Modules - Daniel Ruoso - CppNow 2023](https://www.youtube.com/watch?v=_LGR0U5Opdg)
* [CMake: A Case Study - Hans Vredeveld - ACCU 2023](https://www.youtube.com/watch?v=8l53O3FaJdM)
* [Things I Learnt While Trying to Avoid Becoming a CMake Expert - CB Bailey - ACCU 2022](https://www.youtube.com/watch?v=852VSXFaDO0)
* [Modern CMake Best Practices for Library Authors by Alex Reinking - San Diego C++ Meetup 7/11/2023](https://www.youtube.com/watch?v=bemvHlcz1Qc)
* [SD C++ Meetup 2023](https://www.dropbox.com/sh/c1u1g54o3ez7tua/AADe99hgeXXCM2-4NzxamCwBa?dl=0)
* <https://github.com/alexreinking/sdcppmu-diffuse>
* [Building a Dual Shared and Static Library with CMake](https://alexreinking.com/blog/building-a-dual-shared-and-static-library-with-cmake.html)
* <https://github.com/ComicSansMS/cpp_modules_includes>
