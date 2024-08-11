---
layout: post
title: "C++ Should Be"
date: 2024-08-11
tags: c++ c++20 c++23 development
---

## Key observations
* New tools don't make old tools less capable
* We should worry about the longevity of our C++ code

## Why C ?
* Libraries with C interfaces are very accessible (OS, POSIX, OpenGL ...)
* Easy to learn/use
* Low level access without too much fuss
* Fast
* Stable

## Why C++ when Rust?
* There's all that existing C++ code
* There's all that existing "unsafe" C code
* Rust design has a bad tradeoff set for some problems

## Case study: Rust gamedev
* Higher up-front design cost
* Idea exploration not rapid
* Overly abstract

## C++ uniquely fit for
* Abstracting low level C stuff (Embedded, Real Time)
* Scientific computing
* Performance-critical rapid prototyping

## Please do
* Write simple idiomatic code
* Use simple libraries
* Use other tools when warranted
* Advocate for less churn in the committee

## Please don't
* Make this language more complex
* Veer from core principle like generic programming
* Try to make C++ into other languages

## References
* [C++ Should Be C++ - David Sankel - C++Now 2024](https://www.youtube.com/watch?v=qTw0q3WfdNs)
* [Leaving Rust gamedev after 3 years](https://loglog.games/blog/leaving-rust-gamedev/)
