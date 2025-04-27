---
layout: post
title: "C++ HFT Optimizations"
date: 2025-04-27
tags: c++ performance design
---

## Avoid context switches and bypass the scheduler

## Divide threads to three tiers
* Real time threads - low latency. Isolated, pin to a dedicated core, spin
* Admin threads - high priority. Isolated, pin to group
* System processes - low priority, low load. Non isolated

## Networking kernel bypass
* Kernel
* [OnLoad](https://github.com/majek/openonload/blob/master/README)
* [TCP Direct](https://github.com/Xilinx-CNS/tcpdirect)
* [EF_VI](https://github.com/majek/openonload/blob/master/README.ef_vi)

## The most important optimization - cache warming

## Nothing is optimization unless measured

## Beware microbenchmarking
* Make sure you measure the correct thing
* Make sense of the results
* Always measure your app and in a real scenario

## Sharing data between threads

### Find Relaxations
* Whole structure must be atomic - is_always_lock_free
* Can we fail the update
* Are updates dependent on each other
* Number of readers/writers
* Realtime thread is reader or writer

### Takeaways
* Take advantage of any relaxation you have
* Use the most specific data structure

## Lock free queue types
* Consumers - single, multi
* Producers - single, multi
* Pop on empty - return false, return sentinel
* Push when full - return false, overwrite
* Favour - readers, writers

## Key design concepts
* Single producer, multi consumer
* Producers count is known at compile time
* Favour writers
* Reduce writers sharing
* Reduce reader/writer sharing
* Improve memory ordering

## Example
<https://gitlab.com/qspark-public/sclfq>

## Reference
* [Optimizations in the HFT world :: Yossi Moalem, Assaf Wolfhart](https://www.youtube.com/watch?v=KHlI5NBbIPY)

