---
layout: post
title: "Handling ABI by Package Managers"
date: 2022-05-21
tags: c++ development design ci cd abi
---

## Package manages assumptions
* 1:1 relationship between source code and binary (per platform) - Good for reproducability
* Binaries should be as portable as possile - Bad for performance
* Toolchain is the same across the ecosystem - One compiler, one set of rutime libraries is not flexible enough

## API: Application Programming Interface
* Function names and types as written in the source
* Enforced at compile time
* Incompatibilities generally fail at compile time

## ABI: Application Binary Interface
* Calling conventions
* Function name mangling
* Data types and sizes
* Layout of structures
* Incompatibilities may fail at link time, or give errors at runtime

## ABI consistency is guaranteed if you build everything with:
* Consistent API
* Same compiler
* Same flags

## Bundled Distribution

### Examples
* Linux distributions (Red Hat, Debian)
* E4S, xSDK, Anaconda
* Spack with locked versions

### Idea
* Curate a large set of mutually compatible dpendnecies

### Pros
* Stability

### Cons
* Infrequent updates
* High packaging/curation effort
* Lack of flexibility

## Semantic Versioning 

### Examples
* Spack, Conan, vcpkg, NPM, Cargo, Go
* Most language dependency managers

### Idea
* Use uniform vesrsion convention
* Solve for compatible set 

## Pros
* Frequent updates
* Only relies on local information
* Work in theory

### Cons
* Versions are coarse
* Developers over-constrain/over-promise
* Errors strat to dominate at scale

## Live at Head

### Examples
* Google, Facebook, Twitter

### Idea
* Everything in one repository
* Developers test changes with all dependents

### Pros
* Frequent updates
* Stability, consistency
* All changes tested

### Cons
* Doesn't scale beyond a single organisation
* High computational cost of testing
* Lack of flexibilty (typically just one target env.)

## Package Manager
* Manages dependency relationships
* Feteches artifacts for build
* Drives package-level build systems

## High-level build system
* Cmake, Autotools
* Hanle library abstractions
* Generate Makefiles, etc.

## Low-Level Build System
* Make, Ninja
* Handles dependnecies among commands and files in a single build

## References
* "Software Engineering at Google" _Titus Winters, Tom Manshreck, and Hyrum Wright_ O’Reilly 2020
* [How Can Package Managers Handle ABI (In)compatibility in C++? - Todd Gamblin - CppCon 2021](https://www.youtube.com/watch?v=gWe2K_oCp6A)
