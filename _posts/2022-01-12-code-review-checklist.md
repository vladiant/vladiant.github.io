---
layout: post
title: "Code Review Checklist"
date: 2022-01-12
tags: development c++
---

## Item to Check

### Coding Styles
* Assertions properly used?
* Avoid providing implicit conversions

### Design
* Component design available?
* Current interface and documentation conforms to design description?
* Separation concern
* Are there  cyclic dependencies
* Level of abstraction adequate?

### Verification
* Compile warnings left?
* Lint message count known?
* Are there component tests?
* Are there unit tests?
* Is test coverage full enough?
* Are tests documented / implemented? Are there open test cases?
* Tests performed? Successful?

### Documentation
* Doxygen API documentation available? Descriptions complete?
* Current state of documentation
* Code comments appropriate? Workarounds marked as such?
* Ticket contents comprehensive? General issues communicated to other projects?
* Perforce Changelist contents comprehensive? Only one cause of work? 

### Code Quality
* No deadlocks
* No magic numbers
* Global declarations minimized (comment if needed)
* Proper encapsulation (private access maximized)
* Code robust
* Dead Code
* Assertions
* Debug Messages

### Quick checklist to avoid common mistakes
* Thread save
* Memory
* Locking mechanisms

## General Findings
