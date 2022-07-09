---
layout: post
title: "Real-time C++ Programming"
date: 2022-07-09
tags: c++ development memory debug performance
---

## Use cases
* High-frequency trading
* Embeddded devices
* Video games
* Audio processing (1-10ms)

## "Real-time" programming
* On a normal, non-realtime OS kernel (Windows, macOS, iOS, Android)
* Cross-platform (portability!)
* On a normal consumer machine
* Using a normal C++ implementation (msvc, clang, gcc)
* Only parts of the program are subject to "real-time" constaints, others (e.g. GUI) are not

## "Real-time safe code"
* The worst-case execution time is:
  - deterministic
  - (in principle) known in advance
  - independent on application data
  - Shorter than the given deadline
* The code does not fail
* Don't call anything that might block (non-deterministic execution time + priority inversion!)
  - don't try to acquire a mutex
  - don't allocate / deallocate memory
  - don't do any I/O
  - don't interact with the thread scheduler
  - don't do any other system calls
* Don't call any 3rd party code if you don't know what is is doing
* Don't use algorithms with > O(1) complexity
* Don't use algorithms with amortised O(1) complexity

## "Real-time safe"
* No locks
* No OS calls
* No allocations / deallocations
* No exceptions
* No I/O
* No algortihms > O(1)

## "Real-time safe" parts of the C++ standard library
* The standard says nothing about the execution time
* The standard does not say "does not allocate memory"
  - Infer from specifications
  - Check "might invalidate iterators", "if there is not enough memory"
* The standard does not say "does not use locks"
  - "may not be accessed from multiple threads simultaneously"
  - "May not introduce data races"

## Ecexptions are not "real-time" safe.
* Enter and leave a try block when no exception is thrown is "real-time" safe.

## "Real-time safe" STL algorithms
* Element type / iterator type are "real-time safe".
* Not mentioned by standard.
* For most of them optimal implementation does not require additional allocations.

## Not "Real-time safe"
* [std::stable_sort](https://en.cppreference.com/w/cpp/algorithm/stable_sort)
* [std::stable_partition](https://en.cppreference.com/w/cpp/algorithm/stable_partition)
* [std::inplace_merge](https://en.cppreference.com/w/cpp/algorithm/inplace_merge)
* [std::execution::parallel_*](https://en.cppreference.com/w/cpp/algorithm/execution_policy_tag)

## "Real-time safe" STL containers
* [std::array](https://en.cppreference.com/w/cpp/container/array)
* others are not

## STL containers with custom allocators
* general purpose ([tcmalloc](https://google.github.io/tcmalloc/overview.html), [rpmalloc](https://github.com/mjansson/rpmalloc)) are not "real-time safe"
* "real-time safe" allocator
  - constant time
  - single threaded
  - only use memory allocated uprfornt
* Consider
  - [std::array](https://en.cppreference.com/w/cpp/container/array)
  - [std::pmr::monotonic_buffer_resource](https://en.cppreference.com/w/cpp/memory/monotonic_buffer_resource)
  - [std::pmr::polymorphic_allocator](https://en.cppreference.com/w/cpp/memory/polymorphic_allocator)
  - [std::pmr::vector](https://en.cppreference.com/w/cpp/container/vector), [sample_benchmark](https://quick-bench.com/q/ylppu2cug3S25q1xGrRCGdTEjd4)
  - [std::pmr::unsynchronized_pool_resource](https://en.cppreference.com/w/cpp/memory/unsynchronized_pool_resource/unsynchronized_pool_resource)

## Better: static_vector
* smaller
* faster (no indirection)
* no need to construct allocator object outside vector
* [Boost implementation](https://www.boost.org/doc/libs/1_58_0/doc/html/boost/container/static_vector.html)

## "Real-time safe" utilities
* [std::pair](https://en.cppreference.com/w/cpp/utility/pair)
* [std::tuple](https://en.cppreference.com/w/cpp/utility/tuple)
* [std::optional](https://en.cppreference.com/w/cpp/utility/optional)
* [std::variant](https://en.cppreference.com/w/cpp/utility/variant) ( [boost::variant](https://www.boost.org/doc/libs/1_61_0/doc/html/variant.html) is not!)

## Not "Real-time safe" utilities - use type erasure
* [std::any](https://en.cppreference.com/w/cpp/utility/any)
* [std::function](https://en.cppreference.com/w/cpp/utility/functional/function)

## Lambdas 
* "Real-time safe"

## Coroutines
* Not "Real-time safe" 
* Possible dynamic allocation

## Any syncronization primitives except std: 
* Not "Real-time safe"

## [std::atomic](https://en.cppreference.com/w/cpp/atomic/atomic) - "Real-time safe"
* Use on its own
* Lock-free queues
* Spinlocks
* Make sure it is lock-free! ([std::atomic<T>::is_always_lock_free](https://en.cppreference.com/w/cpp/atomic/atomic/is_always_lock_free))

## Random number generators
* [std::rand](https://en.cppreference.com/w/cpp/numeric/random/rand) - Not "Real-time safe"
* Others too - amortised complexity
* [Xorshift](https://en.wikipedia.org/wiki/Xorshift) - maybe, not in standard
* Algorithms for distributions - implementation defined, not "Real-time safe"

## References
* [Real-time Programming with the C++ Standard Library - Timur Doumler - CppCon 2021](https://www.youtube.com/watch?v=Tof5pRedskI)
* [Implementing static_vector: How Hard Could it Be? - David Stone - CppCon 2021](https://www.youtube.com/watch?v=I8QJLGI0GOE)
