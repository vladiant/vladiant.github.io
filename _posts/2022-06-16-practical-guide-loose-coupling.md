---
layout: post
title: "Guide To Loose Coupling"
date: 2022-06-16
tags: c++ design
---

## The Essence of Good Design
* Good Design is Easier to change than Bad Design
* Flexible
* Scalable - Easy to extend, maintain, reuse
* Testable

## Loose Coupling -> Easier To Change

## KISS
* Keep It Simple

## STUPID
* Singleton
* Tight Coupling
* Untestability
* Premature Optimization
* Indescriptive Naming
* Duplication

## Law of demeter
** Only talk to your immediate friends!

## How to fix it?
* By applying SOLID principles the proper way!
* By applying Test Driven Development (TDD) / Behaviour Driven Development (BDD)!

## SOLID vs STUPID
Let us fix it:
* Single Responsibility Principle - Consider classes to have only one reason to change

### Dependency Injection
* C++ constructors
* inject singletons there
* consider passing initialized objects instead of parameters to initialize them
* prefer composition over inhertiance
* Consider using strong types for strong interfaces

### Polymorphysm in C++
* Inheritance
* Type-Erasure
* std::variant / std::any
* Templates
* Concepts

## Consider using proper abstractions for your project
* Templates / Concepts - Dependencies know at compile time
* Type Erasure - Run-Time dependency
* Inheritance - Never?

## Reference
* [Law of Demeter: A Practical Guide to Loose Coupling - Kris Jusiak - CppCon 2021](https://www.youtube.com/watch?v=QZkVpZlbM4U)
