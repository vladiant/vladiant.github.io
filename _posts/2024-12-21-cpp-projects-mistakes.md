---
layout: post
title: "C++ Project Mistakes"
date: 2024-12-21
tags: c++ design development 
---

## Recommendations

### Mistake: Unclear Project "Contracts"
* Is this a "real" project?
* What is for?
* How does it compare to "other_project"?
* Is this project supposed to build this way?

#### Instead: Have a README
* Describe the interfaces of your project there
* While your are at it, add the other basics
    - Introduction
    - Goals and scope
    - Developer documentation
    - contributing guide

### Mistake: Inconsistent/Claimed Project Name
* Your project needs to be well-identified - when downloaded, released, signed
    * ⚠️ Names like util and db
    * ⚠️ Three-letter-acronyms!
    * ❌ Incomplete forking
    * ❌ Ad-hoc vendoring
    * ⚠️ Changing names =~ forking

#### Instead: Do some homework
Looking for "zerocode" in arbitrary C++ packaging ecosystems:
* [ArchLinux AUR](https://aur.archlinux.org/): none
* [vcpkg](https://vcpkg.io/en/): none
* [Conan Center](https://conan.io/center): none
Verdict: Seems unclaimed!

Other languages?
* <https://crates.io/>: none
* [PyPI](https://pypi.org/): none

### Mistake: Neglecting Library Filenames
What: zerocode given libzerocode.a or libzerocode.so
- ⚠️ -L/usr/lib -libzerocode.debug
- ❌ -L/usr/lib -lzero/code
- Header-only libraries claim their filenames!

#### Instead: Name your library files after your project!
- ✅ L/usr/lib -lzero-code
- ✅ L/usr/lib -lzero_code
- ✅ L/usr/lib -lzerocode
- ✅ L/usr/lib/debug -lzerocode
- ✅ /usr/lib/libzerocode.a
Assume case insensitive filesystems!

### Mistake: Ignoring Users with Build Systems
* Hi! We'r almost everyone!
* We reference your project in our build configurations
* No ecosystem-wide interop yet

#### Instead: Define a Build System Identity
How do build systems describe you as dependency?
* zerocode::zerocode from zerocode-config.cmake
* zerocode maps to zerocode.pc

If you CMake:
* install(EXPORT ... namespace zerocode::)

If you don't:
* Consider generated CMake anyway
* Ship pkg-config metadata if you target POSIX
* Help drive convergence: <https://github.com/cps-org/cps>  

### Mistake: Unconsidered Header Identity
These are all "valid" references to one header
* /usr/include/zerocode/core.hxx
Contents of libzerocode-dev!:
```
#include <zerocode/core.hxx>
#include <core.hxx>
```

#### Instead: Namespace your headers
- ✅ #include <zerocode/core.hxx>
- ✅ #include "zerocode.h"
- ⚠️ #include "config.h"
- ⚠️ #include "core/utils.h"
- ⚠️ #include <utils>

* Ensure "zerocode/core.hxx" exists in your repo!
* Be consistent in your codebase!

### Mistake: Invented/Ambiguous File Extension
* How do identify file as Java, Python, Go, ... ?
* Ask the build system? Best-effort lexxing?

#### Instead: Use a Language-Specific File Extension
Define your files as being implemented in a specific language 
* ✅ zerocode.cxx
* ✅ zerocode.hpp
* ✅ zerocode.c
* ⚠️ zerocode.h
* ❌ zerocode
* ❌ zerocode.codegen

### Mistake: No Correctness Contracts
* Usefulr projects will get ported, patched
* We need support helping determine correctness
    - Users
    - Package maintainers
    - Contributors
* Modern build system have standard test hooks!

#### Instead: Provide tests
* Some accurate, reliable tests are better than nothing
* Define at least the contracts you can commit to
* If someone patches your project, did anything break?

### Mistake: Little/No Build Support
* ❌ No build instructions
* ❌ Source files and a README
* ⚠️ Bespoke build systems (like Makefiles)

#### Instead: Have a Build System
* If you don't have strong opinion, use CMake
    * ✅ Portable
    * ✅ Minimal dependency list
    * ✅ Test workflow
    * ✅ Install workflow
    * ✅ Packaging integrations
* Otherwise have a simple project structure

### Mistake: Overspecifying Build Rules
Many choices must to be made before environment provision
* Architecture tuning
* dependency pinning
* Compilation toolchain
* Standard version
* Thread sanitizer
* [Hyrum's law](https://www.hyrumslaw.com/)

### Mistake: Overspecifying Build Rules - CMake Edition
* ❌ Hardcoding CMAKE_* variables
* ⚠️ Fiddling with build types in CMakeLists.txt

#### Instead: Defer to "Higher Level" Contexts
* Invest in dependency management tools
    - Monorepo
    - Packaging system
* Inject more into your build
    - CXXFLAGS and LDFLAGS
    - CMake toolchain files
* Analogous : Inversion of Control

### Mistake: Treating Warnings as Errors
* ⚠️ What does "all warnings are errors" mean?
* ⚠️ What about flaky "-Wall" warnings?
* ❌ Have you tested that specifically? What about new compilers to come?

#### Instead: Allow Choice Per Workflow
* ✅ Support in build system instead
    - [COMPILE_WARNING_AS_ERROR](https://cmake.org/cmake/help/latest/prop_tgt/COMPILE_WARNING_AS_ERROR.html)
* ✅ Use [CXXFLAGS](https://cmake.org/cmake/help/latest/envvar/CXXFLAGS.html) to match [CXX](https://cmake.org/cmake/help/latest/envvar/CXX.html)
* ✅ Drive diagnostics from `compile_commands.json` - [CMAKE_EXPORT_COMPILE_COMMANDS](https://cmake.org/cmake/help/latest/variable/CMAKE_EXPORT_COMPILE_COMMANDS.html)

## References
* [Mistakes to Avoid When Writing C++ Projects - Bret Brown - C++Now 2024](https://www.youtube.com/watch?v=UrU8O1mMyNE)
* <https://github.com/bretbrownjr/zerocode>
* <https://github.com/cps-org/cps>