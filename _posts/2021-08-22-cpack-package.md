---
layout: post
title: "CPack Package Generation"
date: 2021-08-22
tags: c++ cmake make
---

## CMake snippet
```
# Set it according to your needs
include(InstallRequiredSystemLibraries)

set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "My funky project")
set(CPACK_PACKAGE_VENDOR "Me, myself, and I")
set(CPACK_PACKAGE_DESCRIPTION_FILE "${CMAKE_CURRENT_SOURCE_DIR}/ReadMe.txt")
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/Copyright.txt")
set(CPACK_PACKAGE_VERSION_MAJOR "1")
set(CPACK_PACKAGE_VERSION_MINOR "3")
set(CPACK_PACKAGE_VERSION_PATCH "2")
set(CPACK_PACKAGE_INSTALL_DIRECTORY "CMake ${CMake_VERSION_MAJOR}.${CMake_VERSION_MINOR}")
if(WIN32 AND NOT UNIX)
  # There is a bug in NSI that does not handle full UNIX paths properly.
  # Make sure there is at least one set of four backlashes.
  set(CPACK_PACKAGE_ICON "${CMake_SOURCE_DIR}/Utilities/Release\\\\InstallIcon.bmp")
  set(CPACK_NSIS_INSTALLED_ICON_NAME "bin\\\\MyExecutable.exe")
  set(CPACK_NSIS_DISPLAY_NAME "${CPACK_PACKAGE_INSTALL_DIRECTORY} My Famous Project")
  set(CPACK_NSIS_HELP_LINK "http:\\\\\\\\www.my-project-home-page.org")
  set(CPACK_NSIS_URL_INFO_ABOUT "http:\\\\\\\\www.my-personal-home-page.com")
  set(CPACK_NSIS_CONTACT "me@my-personal-home-page.com")
  set(CPACK_NSIS_MODIFY_PATH ON)
else()
  set(CPACK_STRIP_FILES "bin/MyExecutable")
  set(CPACK_SOURCE_STRIP_FILES "")
endif()
set(CPACK_PACKAGE_EXECUTABLES "MyExecutable" "My Executable")
include(CPack)
```

## CMake snippet DEB package
```
set(CPACK_GENERATOR "DEB")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "David Doria") # required

include(CPack)
```

* To use:

```
$ make package
$ sudo dpkg -i DistanceBetweenPoints-0.1.1-Linux.deb
```

## References
* [cpack](https://cmake.org/cmake/help/latest/manual/cpack.1.html)
* [CPack](https://cmake.org/cmake/help/latest/module/CPack.html)
* [CPack DEB Generator](https://cmake.org/cmake/help/latest/cpack_gen/deb.html#cpack_gen:CPack%20DEB%20Generator)
* [DEB](https://gitlab.kitware.com/cmake/community/-/wikis/doc/cpack/examples/linux/DEB)
* [Packaging With CPack](https://gitlab.kitware.com/cmake/community/-/wikis/doc/cpack/Packaging-With-CPack)
* [PackageGenerators](https://gitlab.kitware.com/cmake/community/-/wikis/doc/cpack/PackageGenerators)
* [Cpack Getting Started Guide](https://developpaper.com/cpack-getting-started-guide/)
* [CPack Example](https://github.com/uilianries/cpack-example)
* [Auto-Detect Dependencies when Building .debs Using CMak](https://www.guyrutenberg.com/2012/07/19/auto-detect-dependencies-when-building-debs-using-cmake/)

