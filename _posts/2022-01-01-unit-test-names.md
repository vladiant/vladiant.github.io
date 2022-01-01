---
layout: post
title: "Unit tests naming"
date: 2022-01-01
tags: test
---

## Problems
* Not to have clear explanation of ```_SUCCESS``` and ```_UNSUCCESS``` meaning.
* Not to have single ```_UNSUCCESS``` while all other cases are ```_SUCCESS```.
* In two different cases the method returns ```true``` and ```false``` respectively, but the test name finishes with ```_SUCCESS```.

## Proposed template
* ```TestedMethodName_Scenario_ExpectedBehavior```, where:
  * ```TestedMethodName``` - the name of the method we need to test or the unit of work.
  * ```Scenario``` - Concise description of the data which is sent to the tested method or unit of work.
  * ```ExpectedBehavior``` - The expected outcome of the method or unit of work.

## References
* [7 Popular Unit Test Naming Conventions](https://dzone.com/articles/7-popular-unit-test-naming)
* [The fundamentals of unit testing: Arrange, Act, Asser](http://defragdev.com/blog/?p=783)
