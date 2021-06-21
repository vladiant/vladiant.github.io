---
layout: post
title: "Continuous Integration Notes"
date: 2021-06-21
---

## Motivation
* Avoids “It works on my machine” scenario
* Automatically run the unit and integration tests

## Goals
* Easy to maintain toolcahins
* Concise but powerful config
* Locally runnable CI jobs

## Main tool
* Build system: [Make](https://www.gnu.org/software/make/)
* Build system generator: [CMake](https://cmake.org/)
* Make is a well known tool to anyone working with C/C++ projects. It’s responsible for compiling the entire source code of a project, and it allows for great customization and extensibility by allowing each user to write their own compilation rules.

## Continuous Integration Frameworks
* [Jenkins](https://www.jenkins.io/)
* [AppVeyor](https://www.appveyor.com/)
* [Travis](https://travis-ci.org/)

## Sample projects
* <https://github.com/Algorithms-and-Data-Structures-2021/cpp-cmake-testing-project-template>
* <https://github.com/bsamseth/cpp-project/>

## References
* <https://workwiththebest.intraway.com/blog-post/ci-c-continuous-integration/>
* <https://buddy.works/docs/quickstart/cpp>
* [Cherno about Jenkins and hosting](https://www.youtube.com/watch?v=FHPtchw-eHA)
* [Introduction of Docker](https://manu343726.github.io/2018-09-09-cpp-ci-docker-intro/)
* [Git hook example](https://github.com/kbenzie/git-cmake-format)
