---
layout: post
title: "C++ API Design"
date: 2023-02-12
tags: api design interface
---

## Never return a raw pointer
* Raises questions: _Who owns it? Who deletes it? Is it a singleton global?_
* Consider some kind of wrapper (owning_ptr, non_owning_ptr)  to document intent.

## Consistent Error Handling
* One consistent method of reporting errors in your library.
* Strongly avoid out-of-band reporting (get_last_error() or errno)
* Make error impossible to ignore (no returning an error code!)
* Never use [std::optional](https://en.cppreference.com/w/cpp/utility/optional) to indicate an error condition.
* Consider [std::expected](https://en.cppreference.com/w/cpp/utility/expected)

## Avoid easily swappable parameters
* Two (or more) parameters beside each other of the same type are easy to swap.
* clang-tidy has [bugprone-easily-swappable-parameters](https://releases.llvm.org/13.0.0/tools/clang/tools/extra/docs/clang-tidy/checks/bugprone-easily-swappable-parameters.html)

## Avoid implicit conversions / use strong types

## Fuzz your interfaces
* Should be run with something like address/undefined sanitizers enabled
* Uses your API in ways you never would
* Can be used with any API with creativity
* Help discover patterns of misuse internal to your API

## Summary
* Use better naming
* Use [[nodiscard]] (with reasons) liberally. Any non-mutating function should be.
* Never return a raw pointer
* Use noexcept to help indicate what kind of error handling is being used
* Provide consistent, impossible to ignore error handling with in-band reporting of what went wrong
* Use stronger types, avoid implicit conversions, use explicit constructors
* Avoid default conversions
* (Sparingly) delete problematic overloads / prevent conversions
* Avoid passing pointers (only to be used for single / optional objects)
* Avoid passing smart pointers
* Enable constexpr unless you have really good reason not to

## Reference
* [Back to Basics: C++ API Design - Jason Turner - CppCon 2022](https://www.youtube.com/watch?v=zL-vn_pGGgY)