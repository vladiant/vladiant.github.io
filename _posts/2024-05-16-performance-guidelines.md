---
layout: post
title: "Performance Guidelines"
date: 2024-05-16
tags: c++ performance development
---

## Benchmark Notes
* Benchmarks run on dedicated machine
* GCC 12.1, C++20
* vector vs list vs deque

## Tested
* push_back (tested for move too)
* random_insert
* random_remove
* fill_front
* sorting

## Tested for types
* NonTrivialStringMovable
* NonTrivialStringMoveDeleted
* NonTrivialStringMovableNoExcept

## When to use deque
* To either add or delete from both ends

## When to use vector
* When insertion or deletion are required mostly at the end

## When to use list
* Huge data set

## Takeaways
* The results my differ from OS to another
* No one-size-fits-all solution
* Use reserve whenever possible
* When element size is large, consider list for sorting. No advantage of spatial locality
* Use noexcept if your method don't throw
* Move calculation to compilation as much as possible 
* Use views objects

## Usable features
* [if constexpr](https://en.cppreference.com/w/cpp/language/if)
* [std::is_constant_evaluated](https://en.cppreference.com/w/cpp/types/is_constant_evaluated)
* [consteval](https://en.cppreference.com/w/cpp/language/consteval)

## References
* [Dor Rozen, Igor Pora-Leonovich :: Performance-related coding guidelines](https://www.youtube.com/watch?v=PGd7vG1CMD0)
