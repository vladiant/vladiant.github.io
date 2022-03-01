---
layout: post
title: "Basics of Profiling"
date: 2022-03-01
tags: c++ performance debug
---

> Here's how I found what was slow.

## Sampling Profiling
* Attach to program, periodically interrupt and record the stack trace
* Sampling frequency is customizable
* Results are statistical averages
* Example tool: [vTune](https://www.intel.com/content/www/us/en/developer/tools/oneapi/vtune-profiler.html#gs.ro815u)
* Only needs to be able to read stack trace
* Minimal debug info is enough
* Works out of the box on any executable
* Inlined functions are usually invisible

## Instrumentation profiling
* Add code hooks to explicitly record metrics
* Can provide both averages and exact breakdown by execution frame
* Not affected by inlining or statistical anomalies
* Example tool: [Optick](https://optick.dev/)
* Requires programmers to add collection macros in tactical places in the code
* Supports adding extra business metadata
* Can fallback on sampling
* Build implications

## Setup goals
* Set up a reproducible scenario
* Measure performance
* Define an objective

## Use the right tool
* Instrumentation (+ some sampling) is the recommended way to go
* Sampling alone is cheaper to start with
* Consider adding instrumentation as an investment

## Best work is no work
* Most efficient code does nothing
* Profiling can highlight useless computations
* No need to dive deep into metrics

## Profiling metrics
* CPU time
* Wait time
* System time

## High CPU time
* Inefficient algorithms or data structures
* Spin locks
* Single threaded code
* Branch misprediction, cache misses

## High wait time
* Disk I/O
* Network calls
* Locks
* Synchronization

## Inefficient algorithms
* Time spent in loops and recursive calls
* Check the Big O
* Can some computations be cached and reused?

## Inefficient data structures
* Times spent in find, insert or `operator[]`
* Easier to spot without inlining
* know your data structures strengths and weaknesses

## Spin Locks
* High spin time in profiler or equivalent tagged functions in instrumented profiles
* Look at the bigger picture and threading model
* Check out talks about concurrency

## Single threaded code
* Low core usage in timeline
* Consider parallel algorithms
* ... or a task scheduler

## Micro-architecutre usage
* High CPI rate
* More and more important on modern CPUs
* Micro-optimziation on large applications is tricky
* Keep for last

## Blocking I/O
* High wait/system time in filesystem or network API
* Can it be put in async thread instead?

## Wait on Mutex or Semaphore
* High wait time on synchronization functions
* Remember: "It shouldn't be called mutex, it should be called bottleneck."
* Consider changing concurrency model

> Deal with inefficient algorithms, data structures and locks first.

## References
* [The Basics of Profiling - Mathieu Ropert - CppCon 2021](https://www.youtube.com/watch?v=dToaepIXW4s)
