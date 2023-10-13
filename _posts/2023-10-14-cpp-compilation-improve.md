---
layout: post
title: "C++ Compilation Time Improvement"
date: 2023-10-14
tags: c++ cmake development design
---

## Reasons for slow compilation
* Archaic build model and `#include` system
* Complicated language - overload resolution, template instantiation, SFINAE ...
* Highly generic and sabstract libraries tend to be bulky
* Not using forward declarations, template instantiations in headers...
* Compilation times not a priority for a low level libraries - includeing standard ones

## Modules
* Limited compiler support
* Require migration
* Promising speedups
* Work in progress

## 1. Low hanging fruits
* Build system - consider [ninja](https://ninja-build.org/)
* `cmake -GNinja; ninja` . `ninja` instead of `make`.
* Linker - [default linker (ld)](https://ftp.gnu.org/old-gnu/Manuals/ld-2.9.1/html_mono/ld.html) and [gold](https://wiki.gentoo.org/wiki/Gold) are slow compared to [lld](https://lld.llvm.org/)
* `lld` is used: `cmake -GNinja -DCMAKE_CXX_FLAGS="-fuse-ld=lld"`
* [mold](https://rui314.github.io/mold.html) is faster (UNIX-like platforms only).
* Avoid recompiling unchanged source files. Common tools - [ccache](https://ccache.dev/), [ccache](https://github.com/mozilla/sccache) (cloud shared compilation cache)
* CMake sample
```
# use ccache if available
find_program(CCACHE_PROGRAM ccache)
if(CCACHE_PROGRAM)
   message(STATUS "Found ccache in ${CCACHE_PROGRAM}")
   set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE "${CCACHE_PROGRAM}")
endif()
```
* [RULE_LAUNCH_COMPILE](https://cmake.org/cmake/help/latest/prop_gbl/RULE_LAUNCH_COMPILE.html) prepends ccache to compiler invocations
* Precompiled headers - see below
* Coalesce multiple source files into fewer larger ones: `cmake -GNinja -DCMAKE_UNITY_BUILD=ON -DCMAKE_CXX_FLAGS="-fuse-ld=lld"`
```
set_target_properties(<target> PROPERTIES UNITY_BUILD ON)
```
* Fine tuning: [SKIP_UNITY_BUILD_INCLUSION](https://cmake.org/cmake/help/latest/prop_sf/SKIP_UNITY_BUILD_INCLUSION.html), [UNITY_BUILD_BATCH_SIZE](https://cmake.org/cmake/help/latest/prop_tgt/UNITY_BUILD_BATCH_SIZE.html), [UNITY_BUILD_CODE_BEFORE_INCLUDE](https://cmake.org/cmake/help/latest/prop_tgt/UNITY_BUILD_CODE_BEFORE_INCLUDE.html) , [UNITY_BUILD_CODE_AFTER_INCLUDE](https://cmake.org/cmake/help/latest/prop_tgt/UNITY_BUILD_CODE_AFTER_INCLUDE.html). Keep small batch size, watch out for missing headers.
* Final resort: hardware

## Precompiled headers
* Using the same PCH for multiple targets built in the same project. Can use PCH with CMake.
* Create `PCH.hpp` file with commonly used includes
* Use `target_precompile_headers(<target> PRIVATE "PCH.hpp")`
* Pick / create a target that all other targets depend from.
* `target_precompile_headers(<base_target> PRIVATE "PCH.hpp")`
* `target_precompile_headers(<other_target> REUSE_FROM <base_target>)`
* Compiler flags have to perfectly match, or PCHs will be ignored!
* Consider making PCHs toggleable through a flag
```
option(SFML_ENABLE_PCH FALSE BOOL
       "TRUE to enable precompiled headers for SFML builds")
```
* Put in `PCH.h` : Commonly used first-party headers, expensive headers ( use [ClangBuildAnalyzer](https://github.com/aras-p/ClangBuildAnalyzer) ) , commonly used standard library / third party headers.

## 2. Profile compilation
* [ClangBuildAnalyzer](https://github.com/aras-p/ClangBuildAnalyzer) - parses clang's `-ftime-trace` output and produces human readable report with actinable information. Run in the build folder.
* Compile everything you want to profile
```
cmake -GNinja -DCMAKE_UNITY_BUILD=ON -DCMAKE_CXX_COMPILER=clang++
      -DCMAKE_CXX_FLAGS="-fuse-ld=lld -ftime-trace"
./ClangBuildAnalyzer.exe --all . analysis.bin
./ClangBuildAnalyzer.exe --analyze analysis.bin > analysis.txt && explorer analysis.txt
```
* Visualt Studio extension - [CompileScore](https://github.com/Viladoman/CompileScore)

## 3. Improve physical design
* Split your software into physically self-contained components (header + source) and limit dependencies between components.
* Levelization - components reside in levels due to their relative physical dependencies. Components at level `N` depend on level `N-1` (and lower).
* Always put the function definition in a `.cpp` file (including `=default`) unless inline is intended.
* Prefer forward declarations to headers for third party libraries.
* [PIMPL](https://en.cppreference.com/w/cpp/language/pimpl) - use for components used infrequently or outside the hot path, for isolating third party components. Do not use for anything that must be cache friendly or part of a hot path.

## Good practices for headers
* Do not rely on transitive inclusion
* Do not rely on header inclusion order
* Do not `#include` unnecessarily. Standard library headers come at a price.
* Group headers together logically
* Sort header groups by dependency levels
* Sort headers in groups alphabetically
* Include fine-grained headers, not catch-all ones
* [include-what-you-use](https://github.com/include-what-you-use/include-what-you-use) - Point [CMAKE_CXX_INCLUDE_WHAT_YOU_USE](https://cmake.org/cmake/help/latest/variable/CMAKE_LANG_INCLUDE_WHAT_YOU_USE.html) to the IWYU executable. Can also just use compilation database via [CMAKE_EXPORT_COMPILE_COMMANDS](https://cmake.org/cmake/help/latest/variable/CMAKE_EXPORT_COMPILE_COMMANDS.html)
```
cmake -GNinja -DCMAKE_UNITY_BUILD=OFF # remember to turn unity builds off
      -DCMAKE_CXX_COMPILER=clang++ -DCMAKE_CXX_FLAGS="-fuse-ld=lld"
      -DCMAKE_CXX_INCLUDE_WHAT_YOU_USE=include-what-you-use
```

## 4. Deal with `windows.h`
* Wrap the inclusions in a separate header.
* Forward declare types.

## 5. Deal with templates
* Prefer `constexpr` functions to template metaprogramming
* Consider run-time polymorphism (e.g. type erasure) instead
* Avoid recursive variadic template instantiation, prefer `...` or fold tricks.
* Prefer `if constexpr` to SFINAE whenever possible
* Define templates in source files whenever possible
* `extern template` - Explicit instantiation declaration. Suppresses implicit generation of object code for a particular template specialization in a TU. Use for non-inline functions. Beware of duplication!
* In the header, place template definition + `extern template` for common specializations
* In the source, place explicit template instantiations for those same specializations. Should be linked.

## Templates - from most expensive to least expensive:
* SFINAE
* Instantiating a function template
* Instantiating a type
* Calling an alias
* Adding a parameter to a type
* Adding a parameter to an alias call
* Looking up a memorized type

## 6. Refactor to separate libraries
* Prefer dynamic linking to static linking (e.g. `-DBUILD_SHARED_LIBS=ON` )

## References
* [Improving C++ Compilation Times: Tools & Techniques - Vittorio Romeo - ACCU 2023](https://www.youtube.com/watch?v=PfHD3BsVsAM)
* <https://github.com/vittorioromeo/accu2023>
* [SFML ccache example](https://github.com/SFML/SFML/pull/2032)
* [target_precompile_headers](https://cmake.org/cmake/help/latest/command/target_precompile_headers.html)
* [set_target_properties](https://cmake.org/cmake/help/latest/command/set_target_properties.html)
* [UNITY_BUILD](https://cmake.org/cmake/help/latest/prop_tgt/UNITY_BUILD.html)
* [CppCon 2016: John Lakos “Advanced Levelization Techniques (part 1 of 3)"](https://www.youtube.com/watch?v=QjFpKJ8Xx78)
* [CppCon 2016: John Lakos “Advanced Levelization Techniques (part 2 of 3)"](https://www.youtube.com/watch?v=fzFOLsFASjU)
* [CppCon 2016: John Lakos “Advanced Levelization Techniques (part 3 of 3)"](https://www.youtube.com/watch?v=NrARQ7rHV-c)
* [C++ Modules and Large-Scale Development - John Lakos, ACCU 2019 ](https://www.youtube.com/watch?v=lGZzN7WZ6EA)
* [Lakos'20: The "Dam" Book is Done! - John Lakos, ACCU 2021](https://www.youtube.com/watch?v=yFZcfIfJUdg)

