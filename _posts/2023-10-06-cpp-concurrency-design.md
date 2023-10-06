---
layout: post
title: "C++ Design for Concurrency"
date: 2023-10-06
tags: c++ design concurrency
---

## Scheduler (Abstraction 1)

## Sender (Abstraction 2)
* Describe work
* Responsible for scheduling work on execution resources (threads, GPUs, ...)
* Sends work to be done in place
* Monad (send a value)

## Receiver (Abstraction 3)
* Where work terminates
* Value channel
* Error channel
* Stopped channel

## Basis of control
* Sequence
* Decision
* Recursion

## To prevent bugs
* Elimininate explicit synchronization
* Eliminate OS-level deadlock
* Eliminate data races

## The Cost
* Use the framework for all synchronization
* Avoid shared mutable state
* Change your design approach

## Framework problems
* There can be data race
* There can be deadlock
* Dropping messages

## Design guidelines
* Focus - Each microservice should be focused on one task
* Independence - Microservices should not overlap in their functionality
* Value Types - For the messages
* Avoid blocking - Replace blocking calls with separate microservices
* State Machines - Each microservice can be modelled as a single-thread state machine

## References
* [Using the C++ Sender/Receiver Framework: Implement Control Flow for Async Processing - Steve Downey](https://www.youtube.com/watch?v=xXncLUD-4bA)
* [Designing for C++ Concurrency Using Message Passing - Anthony Williams - ACCU 2023](https://www.youtube.com/watch?v=J-z4Mf9u-Sc)

