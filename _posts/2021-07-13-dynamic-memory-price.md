---
layout: post
title: "Dynamic Memory Price"
date: 2021-07-13
tags: c++ memory cache allocation performance
---

## Principles of data organization for C++ developers
* Keep your classes small
* Declare data members you access together close to each other
* Keep your small classes in a dedicated vector; avoid processing small classes as a part ot a larger class
(dont use vector of pointers use vector of values)
* Further read: <https://johnysswlab.com/2-minute-read-class-size-member-layout-and-speed/>

## Check memory allocation patterns
* Upfront (embedded and real time OS)
* Allocation in bursts (introduce caching, custom allocator for STL) use good allocator
* Gradual allocation - use good allocator

## Why allocators are slow?
* Allocator - finding the chunk of available memory is not easy task.
* This makes them slow.
* The longer running - the more problem. Memory fragmentation.
* This also leads to allocation failures.

## How to tackle memory fragmentation?
* Use vectors of objects instead of vectors of pointers
* Occasionally restart your program
* Preallocate all the needed memory at the program beginning
* Cache memory chunks. Example - producer/consumer
* Use special memory allocations that promise low fragmentation

## Custom allocators for STL containers
* Allocator implements allocate and deallocate methods
* Excellent choice when multiple small allocations are performed

## Caching memory chunks: Checklist
* Many small chunks or few larger?
* Are allocation and deallocation in the same order?
* Is allocation in one thread and deallocation in another?
* Is program a long running one?

## Criteria for custom allocator:
* allocation speed
* memory consumption
* memory fragmentation
* locality of reference

## Allocators of Linux - measure speed and consumption
* [tcmalloc](https://github.com/google/tcmalloc)
* [jemalloc](https://github.com/jemalloc/jemalloc)
* [mimalloc](https://github.com/microsoft/mimalloc)
* [hoard allocator](https://github.com/emeryberger/Hoard)
* [ptmalloc](https://github.com/hustfisher/ptmalloc)
* [dlmalloc](http://gee.cs.oswego.edu/dl/html/malloc.html)

## Presentation
* [The price of dynamic memory in C/C++](https://www.youtube.com/watch?v=nx8fASr3MK8)

## Links
* [The price of dynamic memory: Allocation](https://johnysswlab.com/the-price-of-dynamic-memory-allocation/)
* <https://github.com/ibogosavljevic/johnysswlab>
* [The true price of virtual functions in C++](https://johnysswlab.com/the-true-price-of-virtual-functions-in-c/)
* [The true price of virtual functions in C++: multivector](https://johnysswlab.com/the-true-price-of-virtual-functions-in-c/#multivector)
* [Process polymorphic classes in lightning speed](https://johnysswlab.com/process-polymorphic-classes-in-lightning-speed/)
* [Array of values: our implementation](https://johnysswlab.com/process-polymorphic-classes-in-lightning-speed/#polymorphic)
* [The effect of switching to TCMalloc on RocksDB memory use](https://blog.cloudflare.com/the-effect-of-switching-to-tcmalloc-on-rocksdb-memory-use/)
