---
layout: post
title: "Parallelism Safety Guidelines"
date: 2022-09-19
tags: concurrency c++11 c++17 c++20
---

## Rule 13 ; CP 21
* Mutexes locked with [std::lock](https://en.cppreference.com/w/cpp/thread/lock) or [std::try_lock](https://en.cppreference.com/w/cpp/thread/try_lock) shall be wrapped with [std::lock_guard](https://en.cppreference.com/w/cpp/thread/lock_guard), [std::unique_lock](https://en.cppreference.com/w/cpp/thread/unique_lock) or [std::shared_lock](https://en.cppreference.com/w/cpp/thread/shared_lock) with [adopt_lock tag](https://en.cppreference.com/w/cpp/thread/lock_tag) within the same scope

## Rule 39 ; CP 110
* Use [std::call_once](https://en.cppreference.com/w/cpp/thread/call_once) to ensure a function is called exactly once (rather than the Double-Checked Locking pattern) 

## Rule 19 ;
* There shall be no code path which results in locking of the non-recursive mutex within the scope when this mutex is already locked
 
## Rule 8 ; 
* Verify resource management assumptions of [std::thread](https://en.cppreference.com/w/cpp/thread/thread) with the implementation of standard library of choice

## References
* [Misra Parallelism Safety-critical Guidelines for C++11, 17, Then C++20, 23 - CppCon 2021](https://www.youtube.com/watch?v=hVv7Nc3f4Jo)
* <https://github.com/ComicSansMS>
* [MISRAC++ParallelConcurrencyHeteroRulesOverviewPhase1](https://docs.google.com/document/d/14E0BYqsH_d7fMKvXvaZWoNWtIC65cYBw0aZp4dlev0Q/edit)
