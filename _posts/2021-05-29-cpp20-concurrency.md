---
layout: post
title: "Concurrency in C++20"
date: 2021-05-29
tags: c++ concurrency c++20
---

## Control tokens
* [std::stop_source](https://en.cppreference.com/w/cpp/thread/stop_source)
* [std::stop_source::request_stop](https://en.cppreference.com/w/cpp/thread/stop_source/request_stop)
* [std::condition_variable_any](https://en.cppreference.com/w/cpp/thread/condition_variable_any)
* [std::stop_callback](https://en.cppreference.com/w/cpp/thread/stop_callback)
* [std::jthread](https://en.cppreference.com/w/cpp/thread/jthread)

## Barriers
* [std::barrier](https://en.cppreference.com/w/cpp/thread/barrier)
* [std::barrier<>::arrive_and_wait](https://en.cppreference.com/w/cpp/thread/barrier/arrive_and_wait)

## Latches
* [std::latch](https://en.cppreference.com/w/cpp/thread/latch)
* [std::latch::arrive_and_wait](https://en.cppreference.com/w/cpp/thread/latch/arrive_and_wait)

## Semaphors
* [std::counting_semaphore](https://en.cppreference.com/w/cpp/thread/counting_semaphore)
* [std::binary_semaphore](https://en.cppreference.com/w/cpp/thread/counting_semaphore)

## Updated atomics
* [std::atomic_ref](https://en.cppreference.com/w/cpp/atomic/atomic_ref)
* [std::atomic(std::shared_ptr)](https://en.cppreference.com/w/cpp/memory/shared_ptr/atomic2)
* [std::atomic(std::weak_ptr)](https://en.cppreference.com/w/cpp/memory/weak_ptr/atomic2)

## Coroutines
* No library support currently - write own code
* [https://github.com/lewissbaker/cppcoro](https://github.com/lewissbaker/cppcoro)

## References
* [Concurrency in C++20 and Beyond - Anthony Williams](https://www.youtube.com/watch?v=UsSmA62eQwY)
* [https://github.com/facebookexperimental/libunifex](https://github.com/facebookexperimental/libunifex)
* [http://www.cplusplusconcurrencyinaction.com/](http://www.cplusplusconcurrencyinaction.com/)
