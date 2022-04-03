---
layout: post
title: "Cmake Checks in C++"
date: 2022-04-03
tags: c++ development cmake
---

## cpplint
```bash
cmake "-DCMAKE_CXX_CPPLINT=path_to/cpplint.py" ..
```

## iwyu
``` bash
cmake "-DCMAKE_CXX_INCLUDE_WHAT_YOU_USE=/usr/bin/iwyu" ..
```

## cppcheck
```bash
cmake "-DCMAKE_CXX_CPPCHECK=/usr/bin/cppcheck;--std=c++17" ..
```

## clang-tidy
```bash
cmake "-DCMAKE_CXX_CLANG_TIDY=/usr/bin/clang-tidy;-checks=*" ..
```

## Snippet

* Simple
```bash
set(CMAKE_CXX_CPPCHECK "cppcheck")
```

* Advanced
```bash
find_program(CMAKE_CXX_CPPCHECK NAMES cppcheck)
if(CMAKE_CXX_CPPCHECK)
    message(${CMAKE_CXX_CPPCHECK})
    list(
        APPEND CMAKE_CXX_CPPCHECK 
            # "--enable=warning"
            # "--inconclusive"
            # "--force" 
            # "--inline-suppr"
            "--quiet"
    )
endif()
```

## References
* <https://stackoverflow.com/questions/51582604/how-to-use-cpplint-code-style-checking-with-cmake>
* [CMAKE_LANG_CPPLINT](https://cmake.org/cmake/help/v3.10/variable/CMAKE_LANG_CPPLINT.html)
* [CMAKE_LANG_CPPCHECK](https://cmake.org/cmake/help/v3.10/variable/CMAKE_LANG_CPPCHECK.html)
* [CMAKE_LANG_INCLUDE_WHAT_YOU_USE](https://cmake.org/cmake/help/v3.10/variable/CMAKE_LANG_INCLUDE_WHAT_YOU_USE.html)
* [CMAKE_LANG_CLANG_TIDY](https://cmake.org/cmake/help/v3.10/variable/CMAKE_LANG_CLANG_TIDY.html)
* [Variables for Languages](https://cmake.org/cmake/help/v3.10/manual/cmake-variables.7.html#variables-for-languages)
