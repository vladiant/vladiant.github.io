---
layout: post
title: "Modern CMake Modules"
date: 2022-01-29
tags: cmake c++ development
---

## CMakeLists.txt Notes
* `pkg-config` first
* `find_package` second
```bash
target_compile_options(
...
PRIVATE
$<$<COMPILE_LANG_AND_ID:CXX,Clang,GNU>:-Werror=return-type>
```

## Pragmatic Recommendations
* Declare your module with ADD_LIBRARY or ADD_EXECUTABLE
* Declare build flags with TARGET_xxx()
* Declare your dependencies with TARGET_LINK_LIBRARIES
* Specify what is PUBLIC and what is PRIVATE

## CMake Workflow
* cmake && cmake --build && ctest && cmake --install
* No magic variables as -DMAGIC_VARIABLE=1
* Do not hijack CMake variables
* Do not require specail build target
* Do not expect certain environments - use find_library, find_program

## Module walktrough
### PlanetExpress.cmake
* "Include Module"
* include(PlanetExpress)
* Found on CMAKE_MODULE_PATH

### FindPlanetExpress.cmake
* "Find Module"
* find_package(PlanetExpress REQUIRED)
* Found on CMAKE_MODULE_PATH

### PlanetExpressConfig.cmake or planet-express-config.cmake
* "Config Package"
* find_package(PlanetExpress REQUIRED) or find_package(planet-express REQUIRED)
* CMAKE_PREFIX_PATH()

## Essential for CMake modules

### API documentation
* static site generators like sphinx
* A great README
   
### Testing
* Test build examples via add_test and CTest
* Consider test fixtures (CMake 3.7) - Craig Scott https://crascit.com/2016/10/18/test-fixtures-with-cmake-ctest/
   
### Printing messages
* message() supports verbosity settings now! (~CMake 3.15)
* cmake --log-level to configure

## Installing a CMake module
* Folder `share/cmake`
* You may ship version files as well

## CMakeLists.txt for CMake modules
```bash
cmake_minimum_required(VERSION 3.21)
project(cmake-planet-express LANGUAGES NONE)
enable_testing()
   
install(
  FILES PlanetExpressConfig.cmake
  DESTINATION share/cmake/PlanetExpress
  COMPONENT cmake-planet-express
)
```

## Development Setup
```bash
export CMAKE_GENERATOR=Ninja
export CMAKE_TOOLCHAIN_FILE=path/to/Toolchain.cmake
export CMAKE_BUILD_TYPE=Debug
export DESTDIR=your/staging/dir
```

## Development Workflow
```bash
git clone https://<host>/cmake-planet-express.git
cmake -B build -S cmake-planet-express
cmake --build build
ctest --test-dir build
cmake --install build --prefix /opt/myorg --component cmake-build-express
```

## Integration Workflow
```bash
git clone https://<host>/cxx-project.git
cmake -B cxx-build -S cxx-project -DPlanetExpress_DIR-./cmake-planet-express
cmake --build cxx-build
ctest --ctest-dir cxx-build
cmake --install cxx-build --prefix /opt/myorg --component cxx-project
```

## Modern CMake less briefly
* [Daniel Pfeifer, Effective CMake (2017)](https://www.youtube.com/watch?v=bsXLMQ6WgIk)
* [Craig Scott , Deep CMake for Library Authors (2019)](https://www.youtube.com/watch?v=m0DwB4OvDXk)
* [Deniz Bahadir, Primer on Modern CMake (2019)](https://www.youtube.com/watch?v=y7ndUhdQuU8)
* [Deniz Bahadir, Update on Modern CMake (2019)](https://www.youtube.com/watch?v=y9kSr5enrSk)

## Reference
* [Modern CMake Modules - Bret Brown - CppCon 2021](https://www.youtube.com/watch?v=IZXNsim9TWI)
