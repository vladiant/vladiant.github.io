---
layout: post
title: "C++ Package Managers"
date: 2022-11-30
tags: c++ development coding debug abi
---

## How ABI is broken?
* Change compiler
* Change compiler version
* Change target OS
* Change target architecture
* Add optinal features to a library

## Package manager have adapted to solve some of these problems
* Breaking ABI
* The diamond problem of dependency management
* Keeping dependencies up to date is important!

## Other benefits of C++ package manager
* Support for building packages from source to overcome ABI compatability issues
* Binary caches that can be downloaded from after a check that rebuild isn't necessary.
* Tight control over package versions (and easy version updates)
* Reproducible build environments (using manifests)
* Large, tested package catalogs
* Support for both open-source and closed-source packages
* Support for downloading packages from offline sources (for organizations disconnected from the open internet)
* Thousands of contributions from open-source contributors all over thw world benefitting your development workflow

## Whey you should consider a package manager?
* When your project has more than 1-2 dependencies, or you have dependnecies on dependencies.
* When you have open source dependencies
* When your project has no dependencies, but you want to implement something that is already available in the public domain
* When you are thinking about making your library header-only because it will make more portable.
* If you are concerned about maintenance or security

## Issues modules will address
* Over-use of headers during preporcessing (assumed no precompiled headers used)
* Macros and "using" declarations (by hiding them away from code outside the module)
* Some ODR violations (separate translation units in separate modules)
* Too many files in your repo
* Code architecure is clearer with separate logic components

## Issues modules will not fix
* Maintaing ABI stability within a dependency graph
* Diamond problems
* Migrating thousands of existing open-source libraries to modules (and even more closed-source ones)

## Types of package managers
* System package manager
* C++ package manager
* Language package manager (non-C++)

## System package managers
* Designed for a particular operating system (OS) distribution.
* Cross-platform projects must have special build logic for different OSes if system package managers are needed
* Packages are installed system-wide
* Packages are typically acquired as-is, though some system package managers support build from source (Pacman)
* Not exclusive to C++ packages or even software development; can install apps, tools and libraries for any workflow
* Don't typically provide first-class integration with build servers - however, since install paths are known defaults, your build system may find packages anyway
* Most popular on Linux

## C++ package managers (vcpkg, Conan)
* Tailored for C++ development with more advanced features
* Have ways to address diamond dependency problems
* Support building packages from source or downloading valid prebuilt binaries
* Support a large variety of open source libraries out-of-the-box
* Also support private libraries
* Support acquizition of build tools, platform SDKs, debuggers and other tools needed for a working C++ environment for cross platform development
* Work across multiple platforms, architectures and compilers

## Non-C++ package managers (NuGet, npm, Cargo, pip)
* A single language package manager being reporposed for use with other programming languages as well
* Useful in limited scenarios
* NuGet (a .NET package manager) is the most common example used by C++ developers
* ScenariosNuGet does not address well:
   * ABI violations/diamond problems: no support for building from source, for different compilers, compiler version target architectures, target OS. Need a separate package for each configuraion.
   * Build system that are not MSBuild
   * Non-Windows operating system
* Since non-C++ language package managers do not address unique C++ requirements, not recommended for C++ except for developers touching C++ assets that have no plans to ever modify them.

## Which type of package manager should you use for C++ packages?
* If you work in or target primarily one system, and you do not update your dependencies frequently use a system package manager
* Else if you work in primarily another programming language, use that language primary package manager.
* If you need a system-specific asset and that package is not easily available in C++ language package manager, use a system package manager.
* Else use a C++ language package manager, which helps you resolve ABI issues, diamond problems, offers you access to much wider variety of C++ packages. Also great for installing per-project dependencies so that other projects can have separate versions of the same dependency.

## Reproducible development environments
* Package managers can do more than just get library dependencies
* C++ developers need tools as well
* System package managers have always offered a wide variety of packages
* More recently, C++ language package managers too
* It is important to be able to bootstrap a C++ development environment in an automated and reproducible way
* This ensures consistency between different dev machines and local dev environments and CI
* Use manifests to declare devtool and library dependencies

## How to manage dependencies well
* Be able to build dependencies from source (if necessary)
* Keep your dependencies up-to-date
* Cross-platform should be first class experience
* Make your build environment reproducible
* Do download prebuilt libraries, if they are verified
* Simplify workflow for authoring and publishing dependencies
* Take advantage of existing open-source solutions
* Enforce ABI requirements across all packages, not one at a time
* Use more than one package manager if it improves your productivity

## Reference
* [C++ Package Manager - C++ Dependencies Don't Have To Be Painful! - Augustin Popa](https://www.youtube.com/watch?v=rrcngYMAJ-w)
