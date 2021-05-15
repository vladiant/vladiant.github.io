---
layout: post
title: "C++ Cross Platform Development"
date: 2021-05-14
---

## Build
* Combination of variants
* The variant combination should be build int own directory
* A variant may be:
  * Base OS
  * Processor architecture
  * GUI
  * Build tools and runtime libraries
  * Facilities
  * Versions (of OS, ...) 
  * Other ...

## Platform differences are variants
* Base OS
* Processor Architecture
* GUI
* Build tools and runtime libraries

## Hiding behind API
* Define internal API with different implementations
* Place different implementations in different directories

## Target hierarchies
* Classify - common/, arch/, os/, gui/ toolset/, etc.
* Arrange source to reflect classification os/win/ce/3.0/src
* Specify target attributes to build system as hierarchy OS=win/ce/3.0

## Depth override
* Search for target-specific version of the source file
* Search in defined order, common last
* If file is not found, drop attribute element from the right of hierarchy and try again
* More specific code is foudn further right of the tree

## Considerations
* Plan to let it evolve
* Be prepared to refactor code
* Write code at the leaves and push up - easy to identify portability work
* Regular automated build/test for all platforms - find problems quickly

## Code 
* Specify category order
* Subcategories can have elements removed until empty
* Don't allow duplicate locations

## Build Systems
* [GNU Make](https://www.gnu.org/software/make/manual/make.html)
* [NMake](https://docs.microsoft.com/en-us/cpp/build/reference/nmake-reference?view=msvc-160)
* [XCode](https://developer.apple.com/xcode/)
* [MSBuild](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild?view=vs-2019)

## CMake
* Most widely used - de facto standard
* Should learn the language and best practices
* Problem - reproduce configuration and build
* Build each from source - [ExternalProject_Add](https://cmake.org/cmake/help/latest/module/ExternalProject.html)
* [find_package](https://cmake.org/cmake/help/latest/command/find_package.html) - Config files: XXXConfig.cmake, [CMAKE_PREFIX_PATH](https://cmake.org/cmake/help/latest/variable/CMAKE_PREFIX_PATH.html)
* [Find modules](https://cmake.org/cmake/help/latest/manual/cmake-developer.7.html) : (not cmake dependent) - FindXXX.cmake, [CMAKE_MODULE_PATH](https://cmake.org/cmake/help/latest/variable/CMAKE_MODULE_PATH.html)
* Packaging: [CPack](https://cmake.org/cmake/help/latest/module/CPack.html)
* Testing: [Ctest](https://cmake.org/cmake/help/v2.8.12/ctest.html)
* Toolchains: [CMAKE_TOOLCHAIN_FILE](https://cmake.org/cmake/help/latest/variable/CMAKE_TOOLCHAIN_FILE.html) , Conan profiles
* [FetchContent](https://cmake.org/cmake/help/latest/module/FetchContent.html) - downloads at configure time, doesn't scale

## Common configuration
* File: CMakePresets.json
* Common configure options and share with others. Integrated in Visual Studio Code
* Example: [https://github.com/WillBuik/pong](https://github.com/WillBuik/pong)
* ACCU 2021 example: [https://github.com/esweet431/box2d-lite](https://github.com/esweet431/box2d-lite)
* [Documentation cmake-presets](https://cmake.org/cmake/help/latest/manual/cmake-presets.7.html)
* [CMakePresets.json and CMakeUserPresets.json Microsoft vendor maps](https://docs.microsoft.com/en-us/cpp/build/cmake-presets-json-reference?view=msvc-160)

## Dependency management
* No automation and reproducible dependency management
* System package managers: apt
* Build system specific package managers: [NuGet](https://www.nuget.org/)
* Language specific package managers: [vcpkg](https://vcpkg.io/en/index.html)
* [Conan](https://conan.io/) -> recommended for C++ cross platform development

## Debugging
* Multiple platform specific debugging tools
* GUI vs Command driven interface
* Core dumb debugging
* Debugging crashes on CI

## Cross platform IDE
* [CLion](https://www.jetbrains.com/clion/)
* [VS Code](https://code.visualstudio.com/)
* [Qt Creator](https://www.qt.io/product/development-tools)

## References
* [Cross-Platform Pitfalls and How to Avoid Them - Erika Sweet](https://www.youtube.com/watch?v=-NhaPNq16Qk)
* [Building and Organising a Multi-Platform Development Code Base - Jim Hague](https://www.youtube.com/watch?v=ch5N6htBZd0)
* [Building Portable C++ Packages: The Curse of Abundance - Piotr Gaczkowski](https://www.youtube.com/watch?v=ibpbrTwnSdU)
* [Building Portable C++ Packages: The Bliss of Unification - Adrian Ostrowski](https://www.youtube.com/watch?v=8nC7ogI-pl8)
* [github.com/Perl/metaconfig](github.com/Perl/metaconfig)
* [doomhammer.info](doomhammer.info)
* [https://github.com/aostrowski](https://github.com/aostrowski)

