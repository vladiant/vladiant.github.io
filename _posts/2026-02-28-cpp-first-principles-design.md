---
layout: post
title: "C++ First Principles Design"
date: 2026-02-28
tags: c++ design
---

## Add new operations to C++ classes
* [Visitor](https://refactoring.guru/design-patterns/visitor)
* [std::visit](https://en.cppreference.com/w/cpp/utility/variant/visit2.html)

## Implement specific functionality
* [Strategy](https://refactoring.guru/design-patterns/strategy)

## What should be done to execute piece of work
* [Command](https://refactoring.guru/design-patterns/command)

## Integrate incompatible interfaces
* [Adapter](https://refactoring.guru/design-patterns/adapter)

## Monitoring thousands of endpoints
* [Observer](https://refactoring.guru/design-patterns/observer)

## Decoupling from implementation
* [Bridge](https://refactoring.guru/design-patterns/bridge)

## Virtual functions performance overhead
* [CRTP](https://en.cppreference.com/w/cpp/language/crtp.html)
* [C++20 concepts](https://en.cppreference.com/w/cpp/language/constraints.html)

## Do you really need inheritance
* [Type Erasure](https://www.modernescpp.com/index.php/type-erasure/)

## General Class Design Tips
* Prefer non-member, non-friend functions - better encapsulations
* Prefer minimality - single purpose classes
* Prefer algorithms which scale well with additional data
* Do not optimize prematurely
* Avoid implicit conversions
* Sequence - prefer vectors
* Allocate memory the right way
* Globals, shared data, static objects increase coupling and reduce scope for parallelism
* Use message queues to communicate instead of shared global data
* Compile at the highest warning level

## References
* [First Principles While Designing C++ Applications - Prabhu Missier - CppCon 2025](https://www.youtube.com/watch?v=8mLo5gXwn4k)
* <https://github.com/pcodex>
