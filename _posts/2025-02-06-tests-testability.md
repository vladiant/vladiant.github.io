---
layout: post
title: "Tests and Testability"
date: 2025-02-06
tags: test design interface development
---

## Unit Tests

### What component is tested?
Tests component in isolation, with external dependencies stubbed out

### What behaviours are tested?
Happy and unhappy paths

### What is the goal?
Verifies that component/class does what is expected

### What is mocked out?
Other components and classes

## Integration tests

### What component is tested?
Component that is running in the expected environment

### What behaviours are tested?
Happy paths. Unhappy paths can be difficult to test.

### What is the goal?
Verifies that component behaves as expected for its expected use case

### What is mocked out?
Other executables or system level dependencies

## System tests

### What component is tested?
Executable deployed to a test environment

### What behaviours are tested?
Happy paths.

### What is the goal?
Verifies functionality when integrated to a production-like system

### What is mocked out?
Nothing

## Design for testability
* Follow SOLID principles
* Library implementer must provide mock objects

## Additional considerations
* The API shouldn't have features that exist only for testing
* API choices shouldn't prevent testing
* We need way to stub out system dependencies

## Techniques
* PIMPL idiom
* Depend only on interfaces
* Adding test APIs via `guards`
* Abstract Factory methods

## Generalized mocking and testing
* Mocking with DI via an abstract interface
* Mocking with DI via a template type
* Responsible for DI : PIMPL

## References
* [Testability and C++ API Design - John Pavan, Lukas Zhao & Aram Chung - C++Now 2024](https://www.youtube.com/watch?v=DiQF7W58Fjs)
