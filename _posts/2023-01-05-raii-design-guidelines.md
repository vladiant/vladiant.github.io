---
layout: post
title: "RAII Design Guidelines"
date: 2022-12-06
tags: c++ design interface
---

## RAII Solves
* Leaks
* Use after disposal
* Double disposal

## RAII not intended to solve
* Resource loops
* Deadlocks

## Example - [std::unique_ptr](https://en.cppreference.com/w/cpp/memory/unique_ptr)
* Custom disposal method - see unique_ptr template argument
* Acquiring a resource handle - .get() - maybe a security hazard

## Design guidelines

### Default acquisition?
* Provide a default constructor to set that up
* Does not preclude an empty state as well
* Destructor may need to understand that resource was released "early"

### "empty state"?
* Example nullptr for std::unique_ptr
* Perhaps provide a default constructor to set that up
* Ensure that your destructor will do the right thing for an empty resource

### Adopting a resource allowed?
* Provide a single parameter constructor (probably explicit) to set that up
* Does not preclude an empty state as well
* Destructor may need to understand that resource was released "early"

### Copyable?
* If not deletete your copy constructor and your copy assignment operator

### Movable?
* If not deletete your move constructor and your move assignment operator

### Access underlying representation?
* Provide a .get() or .native_handle() method to get the raw representation

### Hide underlying representation?
* Provide public member functions to expose the functionality desired withoutexposing the representation
* You may need to allow access to the underlying representation for cases you have not considered

### Dependent resources?
* Provide acquizition functions which return another RAII class instance to manage that dependent resource

### Release the resource?
* Provide a .release() method to get the raw representation and release control
* Mark the .release() method as [[nodiscard]]

## Reference
* [Back to Basics: RAII in C++ - Andre Kostur - CppCon 2022](https://www.youtube.com/watch?v=Rfu06XAhx90)

