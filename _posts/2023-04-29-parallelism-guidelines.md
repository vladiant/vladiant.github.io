---
layout: post
title: "Parallelism Guidelines "
date: 2023-04-29
tags: c++ concurrency development 
---

## Deadlock guidelines
* [CP.20: Use RAII, never plain lock()/unlock()](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-raii)
* [CP.21: Use std::lock() or std::scoped_lock to acquire multiple mutexes](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-lock)
* [CP.22: Never call unknown code while holding a lock (e.g., a callback)](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-unknown)
* [CP.50: Define a mutex together with the data it guards. Use synchronized_value<T> where possible](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-mutex)
* [CP.52: Do not hold locks or other synchronization primitives across suspension points](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rcoro-locks)

## Lifetime guidelines
* [CP.23: Think of a joining thread as a scoped container](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-join)
* [CP.25: Prefer gsl::joining_thread over std::thread](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-detach)
* [CP.26: Don’t detach() a thread](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-detached_thread)

## New guidelines
* 0.4.8 Mutexes locked with std::lock or std::try_lock shall be wrapped with std::lock_guard, std::unique_lock or std::shared_lock with adopt_lock tag within the same scope.
   * [CP.44: Remember to name your lock_guards and unique_locks](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-name)
* 0.4.13 std::recursive_mutex and std::recursive_timed_mutex should not be used
   * [CP.22: Never call unknown code while holding a lock (e.g., a callback)](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-unknown) 
* 0.5.4 Do not use std::condition_variable_any on std::mutex
* 0.6.1 Use only std::memory_order_seq_cst for atomic operations
* 0.12.4 Always explicitly specify a launch policyfor std::async
* 0.12.11 Objects of type std::mutex shall not have dynamic storage duration

## Modfied guidelines
* 0.10.5 Use std::call_once to ensure a function is called exactly once (rather than the Double-Checked Locking pattern)
   * [CP.110: Do not write your own double-checked locking for initialization](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rconc-double)

## MISRA exclusive rules
* 0.4.4 Do not destroy objects of the following types std::mutex , std::timed_mutex , std::recursive_mutex , std::recursive_timed_mutex , std::shared_mutex , std::shared_timed_mutex if object is in locked or shared locked state
* 0.4.11 There shall be no code path which results in locking of the non-recursive mutex within the scope when this mutex is already locked
* 0.4.12 The order of nested locks unlock shall form a directed acyclic graph

## Reference
* [Parallelism Safety-Critical Guidelines for C++ - Michael Wong, Andreas Weis, Ilya Burylov - CppCon22](https://www.youtube.com/watch?v=OD2huQx0Gco)
* [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)
* [CP: Concurrency and parallelism](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#S-concurrency)
