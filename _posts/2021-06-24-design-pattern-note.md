---
layout: post
title: "Design Pattern Note"
date: 2021-06-24
tags: design
---

## Design patterns
* Are about dependencies and abstractions
* Are about intent
* Are not limited to OO programming
* Are not limited to dynamic polymorphism
* Are not outdated nor obsolete
* Are everywhere

## C++ STL examples

### Strategy
* [std::accumulate](https://en.cppreference.com/w/cpp/algorithm/accumulate)

### Command
* [std::for_each](https://en.cppreference.com/w/cpp/algorithm/for_each)
* [std::transform](https://en.cppreference.com/w/cpp/algorithm/transform)

### Iterator
* [Iterator library](https://en.cppreference.com/w/cpp/iterator)

### Adapter
* [std::queue](https://en.cppreference.com/w/cpp/container/queue)
* [std::stack](https://en.cppreference.com/w/cpp/container/stack)
* [std::priority_queue](https://en.cppreference.com/w/cpp/container/priority_queue)

### Decorator
* [std::pmr::monotonic_buffer_resource](https://en.cppreference.com/w/cpp/memory/monotonic_buffer_resource)

### Template Method
* [std::pmr::memory_resource](https://en.cppreference.com/w/cpp/memory/memory_resource)

### Proxy
* [std::vector< bool >](https://en.cppreference.com/w/cpp/container/vector_bool)
* [std::bitset](https://en.cppreference.com/w/cpp/utility/bitset)

### External Polymorphism
* [Concepts library](https://en.cppreference.com/w/cpp/concepts)

### Bridge
* [PIMPL](https://en.cppreference.com/w/cpp/language/pimpl)

### Prototype
* `virtual std::unique<Concept> clone() const = 0`

### Type erasure
* Templated constructor
* Completely non-virtual interface
* External Polymorphism + Bridge + Prototype

## Reference
* [Klaus Iglberger - Design Patterns - Facts and Misconceptions](https://www.youtube.com/watch?v=u5EAJTHPJN8)
* [Design Patterns: Facts and Misconceptions - Klaus Iglberger - CppCon 2021](https://www.youtube.com/watch?v=OvO2NR7pXjg)
  
