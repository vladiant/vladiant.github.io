---
layout: post
title: "C++ Structured Concurrency"
date: 2026-11-11    
tags: c++ concurrency development
---

## Summary
* Concurrent systems can handle complex scenarios of incoming events
* Achieving high performance can mean eliminating helper facilities like threads, stacks and even heap allocations
* Older approaches are error prone and require attention to details
   * Managing object lifetime
   * Handling complex scenarios
   * Errors and cancelation.
* Structured concurrency is a composable low-overhead approach
   * Both coroutines and the senders (std::execution) frameworks provide structured concurrency
   * Both frameworks interoperate - we don't have to choose one.

## Tips
* Import an existing library, don't start from scratch
   * ASIO - inside or out of boost  <https://think-async.com/Asio/>
   * cppcoro - various coroutine building blocks  <https://github.com/lewissbaker/cppcoro>
   * cobalt - boost coroutine library, with asio compatibility   <https://www.boost.org/doc/libs/master/libs/cobalt/doc/html/index.html>
   * Nvidia stdexec - battle-tested senders library   <https://github.com/NVIDIA/stdexec>
   * beman.execution - senders aiming for standard conformance  <https://github.com/bemanproject/execution>
   * beman.net - senders for networking proposed for standartization  <https://github.com/bemanproject/net>
* Keep control of your main-loop if possible
   * asio::io_context::poll - non-blocking task drainer  <https://think-async.com/Asio/asio-1.36.0/doc/asio/reference/io_context/poll.html>

## How to start
* Try coroutines
  * Already in the standard
  * Quite a few libraries exist.
* If current code is non-blocking: consider starting from the root, not leaf
  * start by changing `return` to `co_return`, then consider where to `co_await`.
* If current code is blocking (threads): go from leafs towards to root
  * function-coloring is an issue - be creative.
* Don't fear cancellation
  * If some old code needs to interact with a suspended coroutine - consider cancellation
  * Alternatively be creative with the `co_await` return type (`std::expected` ?)

## References
* [Why Structured Concurrency is the Future of C++ - Roi Barkan](https://www.youtube.com/watch?v=ttoQfPP_Gkg)
* [Why Structured Concurrency is the Future of C++ - Roi Barkan - slides](https://docs.google.com/presentation/d/1tCQD6qSimgOJ_5EZ2pxbvzV6KLynmRaF-R33KzwCCDk/present?slide=id.g39acee9f8e5_0_699)
