---
layout: post
title: "C++ Dependency Problems"
date: 2024-12-26
tags: c++ design development 
---

## Problem 1: ABI incompatible C++ binaries
* Support building from source

## Problem 2: Build times are too long when building from source
* Build a verified binary cache

## Problem 3: Version conflict - the diamond problem
* Version using baselines (combine all used dependencies together to produce version)

## Problem 4: Build open-source dependencies is hard
* Build open source with package manager

## Problem 5: Organization restricts access to online downloads 
* Cache build assets internally

## Problem 6: Security vulnerabilities in open source code
* Monitor, prevent and respond to vulnerabilities

## Problem 7: Duplicated engineering cost to maintain dependencies
* Centralize common tasks

## Problem 8: Difficult to track or report on all dependencies
* Produce SBOMs (Software Bill of Materials) (SPDX and CycloneDX)

## Problem 9: Build toolchain variations across the org
* Global, reproducible builds

## Problem 10: Moving to new solution is complex or too time consuming
* Break large migrations down into smaller milestones

## Summary
* Build C++ dependencies from source
* Establish binary caching where possible
* Organize dependencies + versions into baselines (fixed points in time)
* Use an open-source package manager to save time/effort
* Create an asset cache for sources needed to build dependencies
* Develop a vulnerability monitoring, prevention and response strategy and associated tools/workflows
* Centralize common dependency management tasks, enforce consistency across organization at scale
* Organize dependencies into coherent packages and start producing SBOMs
* Establish a global toolchain policy and build in containers if possible
* Break large migrations down into smaller milestones with a win at each step

## References
* [10 Problems Large Companies Have Managing C++ Dependencies and How to Solve Them - Augustin Popa](https://www.youtube.com/watch?v=kOW74IUH7IA)
* [SPDX Tools](https://spdx.dev/use/spdx-tools/)
* <https://github.com/spdx>
* [CycloneDX](https://cyclonedx.org/)