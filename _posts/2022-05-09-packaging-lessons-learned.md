---
layout: post
title: "Packaging Lessons Learned"
date: 2022-05-09
tags: c++ development design ci cd abi
---

## Bloomberg Packaging Doesn't Look Like:
* Monorepo
* Unified build system
* CI monoculture
* Project structure monoculture
* Single unified release process

## Bloomberg Packaging Do Look Like:
* Mixture of third-party and first-party projects
* Debian package management 
  * apt-get install package
  * Do not touch packages in /usr
  * First party prefix is /opt/bb/
  * Package repositories are curated
* Majority CMake
* pkg-config for inter-project library metadata
* Mostly use prebuild binaries
* Static linking whenever possible

## How Bloomberg Packages C++
* Flexible developer experience
  * Flexibility in build tools, editors, analyzers, IDEs
  * Often off the shelf
* CI enrollment decided per project
* Production package builds are ABI coherent
  * Releases sent into an integration build system
  * Aggresive dependency rebuilds for coherency
  * Transactional changes to prevent broken releases

## Summary
* Independence from specific build systems
* Coherency on how names are used
* Integration baseline, with branching capabilities

## Reference
* [Lessons Learned from Packaging 10,000+ C++ Projects - Bret Brown & Daniel Ruoso - CppCon 2021](https://www.youtube.com/watch?v=R1E1tmeqxBY)
