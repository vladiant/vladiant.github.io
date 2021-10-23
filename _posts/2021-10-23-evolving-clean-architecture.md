---
layout: post
title: "Evolving Clean Architecture"
date: 2021-10-23
tags: design development api
---

## Takeaways
* [KISS](https://en.wikipedia.org/wiki/KISS_principle): Avoid overengineering or overoptimization
* MAGIC to protect your developers
* Enemy data in your [DTO](https://en.wikipedia.org/wiki/Data_transfer_object): Keep them out
* Extract it when it grows: [SRP](https://en.wikipedia.org/wiki/Single-responsibility_principle) or [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
* THE [ONION](https://www.codeguru.com/csharp/understanding-onion-architecture/), [DIP](https://en.wikipedia.org/wiki/Dependency_inversion_principle): Domain agnostic to externals
* TESTS : Let them smash your design.

## Core Principles
1. Passes the tests
2. Reveals intent
3. No duplication
4. Fewest elements

## Modelling data
* Value object - small, immutable data
* [Data Transfer Objects](https://en.wikipedia.org/wiki/Data_transfer_object) - No methods!
* Expose enttities in API

## Organizing Logic
* Extract mappers
* [Facade](https://en.wikipedia.org/wiki/Facade_pattern): Domain services, Domain objects

## References
* [Evolving a Pragmatic, Clean Architecture - A Craftsman's Guide](https://www.youtube.com/watch?v=47OdZ2gqPtU)
* [Simple Design](https://martinfowler.com/bliki/BeckDesignRules.html)
* <https://victorrentea.ro/>
