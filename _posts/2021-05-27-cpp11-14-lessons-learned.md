---
layout: post
title: "C++11/14 Lessons Learned"
date: 2021-05-25
tags: c++ c++11 c++14
---

## Safe Features
* Add considerable value, easy to use, hard to misuse
* C++11
  * Attribute syntax
  * Consecutive >s
  * decltype
  * Defaulted Functions
  * Delegating Ctors
  * Deleted Functions
  * explicit Operators
  * Function static'11
  * Local Types'11
  * long long
  * noreturn
  * nullptr
  * override
  * Raw String Literals
  * static_assert
  * Trailing Return
  * Unicode Literals
  * using aliases
* C++14
  * Aggregate Init '14
  * Binary Literals
  * deprecated
  * Digit Separators
  * Variable Templates

## Conditionally Safe Features
* Add considerable value, but prone to misuse. Require in depth training and additional care
* C++11
  * alignas
  * alignof
  * auto Variables
  * Braced Init
  * constepr functions
  * constexpr variables,
  * Default Member Init
  * enum class
  * extern template
  * Forward References
  * Generalized PODs '11
  * Inheriting Ctors
  * initializer_list
  * Lambdas
  * noexcept operator
  * Opaque enums
  * range for
  * rvalue references
  * Underlying type '11
  * User defined literals
  * Variadic templates
* C++14
  * constexpr functions '14
  * Generic Lambdas
  * Lambda Captures

## Unsafe Features
* Provide value only in the hands of an expert and prone to misuse. Require explicit training on their use cases and pitfalls.
* C++11
  * carries_dependency
  * final
  * inline namespace
  * noexcept specifier
  * Ref-Qualifiers
  * union '11
  * friend '11
* C++14
  * decltype(auto)
  * Deduced return type

## References
* [C++11/14 at Scale - What Have We Learned? - Vittorio Romeo](https://www.youtube.com/watch?v=H8wzuvynV78)
* [Embracing Modern C++ Safely](https://www.amazon.com/Embracing-Modern-Safely-John-Lakos/dp/0137380356)
* [vittorioromeo.info](vittorioromeo.info)
* [github.com/SuperV1234](github.com/SuperV1234)
