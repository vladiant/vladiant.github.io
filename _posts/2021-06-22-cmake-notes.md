---
layout: post
title: "CMake Notes"
date: 2021-06-22
---

## Base CMake commands
* [cmake_minimum_required](https://cmake.org/cmake/help/latest/command/cmake_minimum_required.html)
* [project](https://cmake.org/cmake/help/latest/command/project.html)
* [find_package](https://cmake.org/cmake/help/latest/command/find_package.html)
* [add_subdirectory](https://cmake.org/cmake/help/latest/command/add_subdirectory.html)
* [FetchContent](https://cmake.org/cmake/help/latest/module/FetchContent.html)
* [add_library](https://cmake.org/cmake/help/latest/command/add_library.html)
* [add_executable](https://cmake.org/cmake/help/latest/command/add_executable.html)
* [target_sources](https://cmake.org/cmake/help/latest/command/target_sources.html)
* [target_include_directories](https://cmake.org/cmake/help/latest/command/target_include_directories.html)
* [target_link_libraries](https://cmake.org/cmake/help/latest/command/target_link_libraries.html)
* [set_property](https://cmake.org/cmake/help/latest/command/set_property.html)
* [target_compile_definitions](https://cmake.org/cmake/help/latest/command/target_compile_definitions.html)
* [CTest](https://cmake.org/cmake/help/latest/manual/ctest.1.html)

## CMake Best Practices
* Use modern CMake
* Target and properties oriented approach
* Avoid variables
* Export interfaces, encapsulate the rest
* Use [find_package](https://cmake.org/cmake/help/latest/command/find_package.html) to handle dependencies

## References
* [CGold: The Hitchhiker’s Guide to the CMake](https://cgold.readthedocs.io/en/latest/)
* [An Introduction to Modern CMake](https://cliutils.gitlab.io/modern-cmake/)
* [Professional CMake](https://crascit.com/professional-cmake/)
* [Minimal CMake example](https://github.com/krux02/minimal_cmake_example/blob/master/CMakeLists.txt)
* [It's Time To Do CMake Right](https://pabloariasal.github.io/2018/02/19/its-time-to-do-cmake-right/)
* [Clang-tidy target](https://github.com/polysquare/clang-tidy-target-cmake)
* [Awesome CMake](https://project-awesome.org/onqtam/awesome-cmake)
* <https://github.com/adishavit/cmake_snippets>
* <https://github.com/dev-cafe/cmake-cookbook>
