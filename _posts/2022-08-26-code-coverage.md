---
layout: post
title: "C++ Code Coverage"
date: 2022-08-17
tags: development ci cd cmake
---

## Steps
* Clean project completely (you want a complete rebuild)
* Recompile everything with gcov compile and link flags.
* Use lcov to process initial .gcno files.
* Run all tests.
* Use lcov to process .gcna coverage files.
* Merge the initial and final lcov files (step 3 and step 5).
* Filter lcov output to only include project files.
* Filter lcov output to exclude unit test files, and main.cpp
* Generate html coverage report from final filtered lcov output.

## CMakeLists.txt

```
WORKING_DIRECTORY ${CMAKE_BINARY_DIR}

# Code coverage results with an optimised (non-Debug) build may be misleading
CMAKE_CXX_FLAGS "-g -O0 -Wall -fprofile-arcs -ftest-coverage"
CMAKE_C_FLAGS "-g -O0 -Wall -W -fprofile-arcs -ftest-coverage")

LINK_LIBRARIES(gcov)
```

### Compile_options
```
-fprofile-arcs
-ftest-coverage
```

## Link_options
```
--coverage
```

## Notes
* Run test, generating the corresponding .gcda files.
* In the directory in which files .gcno and .gcda are located do the following:
```
lcov -c -d . -o name.info

lcov --directory . --capture --output-file name.info
lcov --remove name.info 'tests/*' '/usr/*' --output-file name.info.cleaned
```
* Generate the HTML report
```
genhtml  name.info
genhtml -o out name.info --ignore-errors source

genhtml -o name name.info.cleaned
cmake -E remove name.info name.info.cleaned
```

## Links:
* <https://github.com/cmake-modules/lcov/blob/master/coverage.cmake>
* [C++ using GCOV/LCOV in a CMake project – Stack Overflow](https://codeutility.org/c-using-gcov-lcov-in-a-cmake-project-stack-overflow/)
* [Line coverage report using gcov/lcov](https://swarminglogic.com/jotting/2014_05_lcov)
* <https://github.com/britram/libfc/blob/master/CodeCoverage.cmake>
* [Use gcov and lcov to know your test coverage](https://qiaomuf.wordpress.com/2011/05/26/use-gcov-and-lcov-to-know-your-test-coverage/)
* [C# example](https://github.com/zmaillardhw/gh-action-demo/blob/main/.github/workflows/build.yaml)
* [Github action](https://github.com/marketplace/actions/report-lcov)
* [C++ example](https://github.com/f-squirrel/thread_pool)