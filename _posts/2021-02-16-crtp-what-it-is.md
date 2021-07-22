---
layout: post
title: "CRTP: What It Is, Some History and Some Uses"
date: 2021-02-16
tags: c++ template
---

## Highlights
* [Curiously Recurring Template Pattern](https://en.wikipedia.org/wiki/Curiously_recurring_template_pattern)
```cpp
template <class T>
class Base
{
    // methods within Base can use template to access members of Derived
};
class Derived : public Base<Derived>
{
    // ...
};
```
* Allows the base class to safely access methods of derived class via `static_cast<const T*>(this)` or `static_cast<const T&>()`
* Still be careful calling these methods in constructor!

## The video
* [C++ Weekly - Ep 259 - CRTP: What It Is, Some History and Some Uses](https://www.youtube.com/watch?v=ZQ-8laAr9Dg)

## The channel
* [Cᐩᐩ Weekly With Jason Turner](https://www.youtube.com/channel/UCxHAlbZQNFU2LgEtiqd2Maw)
* Every week a new video about 10 minutes long
