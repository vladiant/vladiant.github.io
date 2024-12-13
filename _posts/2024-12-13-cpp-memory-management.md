---
layout: post
title: "C++ Memory management"
date: 2024-12-13
tags: c++ memory cache allocation 
---

## Overview
`top -o RES`
* [MallocInternals](https://sourceware.org/glibc/wiki/MallocInternals)
* [mmap](https://man7.org/linux/man-pages/man2/mmap.2.html)
* [sbrk](https://linux.die.net/man/2/sbrk)

## Memory Leak
* new() without delete
* Keep entries that are no longer needed
* Missing virtual ~Base()
* Circular reference

## Memory leaks: Tools

### bslma::TestAllocator
* [bslma::TestAllocator](https://bloomberg.github.io/bde-resources/doxygen/bde_api_prod/classbslma_1_1TestAllocator.html)
* <https://github.com/bloomberg/bde/>

Advantages:
* fast
* small overhead
* scoped
Disadvantages:
* code changes required
* compile and link required

### Address Sanitizer
Advantages:
* no code change required
* fast
Disadvantages:
* compile and link required
* extra memory cost

### Valgrind (memcheck and massif)
[Memcheck: a memory error detector](https://valgrind.org/docs/manual/mc-manual.html)
[Massif: a heap profiler](https://valgrind.org/docs/manual/ms-manual.html)

Advantages:
* no code change required
* no compile and link required
Disadvantages:
* slow (10-30 times slower)
* extra memory cost
[KDE massif-visualizer](https://github.com/KDE/massif-visualizer)

## Memory leaks: Tips
* "Static" leaks may hide the real issue - we need enough traffic for profiling
* They are all good tools, but for different cases
* Catch the problem in earlier stages - Integrate Address Sanitizer in CI
* Install the tools so we can start profiling easily
* Care about the lifecycle and ownership of what we allocate

## Fragmentation

### External fragmentation
* I have free spaces, but I need to extend the heap
* `1 - LargestAllocableBlock / TotalFreeMemory`
* Most allocations can be done with chunks in bins

### Internal fragmentation
* I allocate a large chunk for a small size
* `1 - AccessedBytes / TotalAllocatedBytes`
* Avoid useless and underused allocations

[mallinfo](https://man7.org/linux/man-pages/man3/mallinfo.3.html)
* Total bytes
* Total in-use allocations
* Total free space
* Largest allocable block

[Valgrind DHAT: a dynamic heap analysis tool](https://valgrind.org/docs/manual/dh-manual.html)

## Defragmentation

### C++
* [CppCon 2017: John Lakos “Local ('Arena') Memory Allocators (part 1 of 2)”](https://www.youtube.com/watch?v=nZNd5FjSquk)
* [CppCon 2017: John Lakos “Local ('Arena') Memory Allocators (part 2 of 2)”](https://www.youtube.com/watch?v=CFzuFNSpycI)

### malloc
* [Malloc Tunable Parameters](https://www.gnu.org/software/libc/manual/html_node/Malloc-Tunable-Parameters.html)
* [jemalloc](https://jemalloc.net/)
* [Scalable memory allocation using jemalloc](https://engineering.fb.com/2011/01/03/core-infra/scalable-memory-allocation-using-jemalloc/)

### OS
* [Buddy memory allocation](https://en.wikipedia.org/wiki/Buddy_memory_allocation)
* [Buddy System – Memory Allocation Technique](https://www.geeksforgeeks.org/buddy-system-memory-allocation-technique/)
* [CppCon 2019: Emery Berger “Mesh: Automatically Compacting Your C++ Application's Memory”](https://www.youtube.com/watch?v=XRAP3lBivYM)

### Long-running stateless system
* start and run for a long time
* receive requests and process them, no state

## Reference
* [https://www.youtube.com/watch?v=y6AN0ks2q0A](https://www.youtube.com/watch?v=y6AN0ks2q0A)
* [Allocator-Aware C++ Type Design - Jonathan Coe - C++ on Sea 2024](https://www.youtube.com/watch?v=hZyJtRY84P4)
* <https://github.com/jbcoe/value_types>
* <https://github.com/jbcoe/allocators>
* [What Programmers Should Know About Memory Allocation - S. Al Bahra, H. Sowa, P. Khuong - CppCon 2019](https://www.youtube.com/watch?v=gYfd25Bdmws)
* [Getting Allocators out of Our Way - Alisdair Meredith & Pablo Halpern - CppCon 2019](https://www.youtube.com/watch?v=RLezJuqNcEQ)






