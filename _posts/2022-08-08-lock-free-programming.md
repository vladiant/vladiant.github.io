---
layout: post
title: "Lock Free Programming"
date: 2022-07-29
tags: c++ concurrency
---

## Testing the lock-free algorithms
1. Define the requirements of the algorithm in a formal way
2. Devise theoretical algorithm (pseudo code)
3. Proof of correctness (by hand or automated theorem prover, e.g. TLA+)
4. Implement algorithm
5. Code review by experts
6. Unit tests to check single-threaded correctness (necessary condition)
7. Multi-threaded stress tests (check invariants, no data structure corruption)
8. Code instrumentation for specific multi-threaded scenarios (open problem ...)
9. Verification tools such as CppMem to check the data races etc. (for small code snippets)

## Our New Friend Compare Exchange
* Allows us to implement useful algorithms to exchange data in a lock-free way
* These techniques are especially useful in real-time systems
* Care must be taken when manipulating data concurrency without locks

Key observations
1. CAS loops are the basis for many lock-free algorithms
2. CAS can only be used on small data (64 bit usually)
3. CAS can be used to transfer memory ownership atomically between threads
4. Lock-free algorithms usually require managing memory and object lifetime carefully
5. We can add information (e.g. counters) to atomically check for cuncurrent modification with CAS

## Disadvantages
* CAS is rather expensive... but so is locking with contention
* Algorithms for simple problems get rather complex
* Lock-free algorithms are hard to test

## Implementation
* <https://github.com/MatthiasKillat/lockfree_demo>

## Notes
* Replacing std::optional - allocates dynamic memory, most likely not lock-free .Replacing with variation that allocates on stack
* The copy/move cosntructor of T needs to be lock-free - Case of trivially copyable types
* memcpy is lock-free but not atomic

## Reference
* [Matthias Killat - Lock-free programming for real-time systems - Meeting C++ 2021](https://www.youtube.com/watch?v=j2AgjFSFgRc)
