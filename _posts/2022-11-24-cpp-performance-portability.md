---
layout: post
title: "C++ Performance Portability Lessons"
date: 2022-11-23
tags: c++ performance coding design
---

## Lesson 1
* Single source compilation for heterogeneous architecture requires some form of "host/device" function attributes.
### Related Expert Lessons
* Function pointers to the same function have different values depending where they are obtained!
* That makes virtual functions fairly tricky to use!

## Lesson 2
* Data structures in compute kernels need to have reference semantics
### Related Expert Lessons
* Proper reference counting is difficult and/or costly across architecure bundaries
* Kokkos simpli waits for all outstanding asynchronous work before deadlocking

## Lesson 3
* Parallel unsequenced loops are the fundamental building block for performance portable code.
### Related Expert Lessons
* Task systems are possible and useful, but tasks need to contain data parallel unsequenced loops to achieve performance.

## Lesson 4
* Execution and Memory Resources need to know about each other.
### Related Expert Lessons
* Portability expressing more subtle memory semantics such as page migration is a concern.
* Types are not necessarily enough - need instances to support multiple discrete GPUs or multiple queues on a single GPU.

## Lesson 5
* Data Layout Mappings need to be configurable and integral part of the API design
### Related Expert Lessons
* Task systems are possible and useful, but tasks need to contain data parallel unsequenced loops to achieve performance.

## Lesson 6
* More and more special hardware capabilities exist - for full performance these need to be leveraged.
### Related Expert Lessons
* Wherever possible expressing access behaviour via descriptive properties is preferable over prescriptive settings (e.g. const RandomAccess vs. TextureCache)

## Lesson 7
* Hardware is hierarchical and algorithms often don't expose enough parallelism on a single order: need to support nested parallelism.
### Related Expert Lessons
* Nested parallelism should have the same syntax and API as the top level parallelism!

## Lesson 7
* Make Simple things Simple - And complex things easier.

## References
* [C++ Performance Portability - A Decade of Lessons Learned - Christian Trott - CppCon 2022](https://www.youtube.com/watch?v=jNGGKFkt4lA)
* <https://github.com/kokkos/kokkos-tutorials/wiki/Kokkos-Lecture-Series>
