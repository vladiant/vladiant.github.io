---
layout: post
title: "Trust C++ Standard Library"
date: 2021-06-09
---

## Know what your library does

* Are there types / functions constexpr enabled?
* What implicit conversions exist?
* Will the function / constructor implicitly allocate?

* Will allocate:
  * vector
  * deque
  * Required to allocate for each node:
    * list
    * map
    * set

* Might allocate (have small object optimizations)
  * string
  * function
  * any

* Never allocate:
  * pair
  * tuple
  * variant
  * optional
  * array (it also has no constructors!!)

* Algortihms that may allocate
  * *stable*
* If algortihm is constexpr enabled (as of C++20) it will never allocate!

## Know they are very well tested and are all open source!

* GCC's (libstdc++)
* clang's (libc++)
* MSVC's

## Read the source code!

* Understand how and why things are implemented when you need to.

## Reference

* [C++ Weekly - Ep 275 - Trust Your Standard Library in 3 Simple Steps](https://www.youtube.com/watch?v=atAd8gzaM1g)
