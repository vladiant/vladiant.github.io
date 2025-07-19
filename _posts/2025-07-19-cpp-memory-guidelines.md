---
layout: post
title: "C++ Memory Guidelines"
date: 2025-07-19
tags: c++ memory performance
---

## 1. Prefer stack allocation when possible

## 2. malloc() is usually fast, except when it isn't

## 3. Prefer third party heap implementation on Windows

## 4. Reserve finaly container size when known rather than rely on geometric growth

## 5. Avoid using reserve() with constant delta in loops

## 6. Prefer output parameters to returns for containers

## 7. Reuse previous allocations when possible

## 8. Prefer memberwise .clear() over assignment to empty struct

## 9. Avoid using alloca() because it is likely to overflow the stack

## 10. Consider monotonic allocators when resources can be scoped and budgeted

## 11. Each feature on your allocator brings you closer to reimplementing malloc()

## Conclusion
* Dynamic allocation comes at an unpredictable runtime cost
* Size-up allocations once and reuse containers as much as possible
* Consider monotonic allocators, but beware of going further

## Reference
* [Heaps Don’t Lie - Guidelines for Memory Allocation in C++ - Mathieu Ropert - ACCU 2025](https://www.youtube.com/watch?v=74WOvgGsyxs)
* <https://github.com/microsoft/mimalloc>
* <https://mropert.github.io/>

