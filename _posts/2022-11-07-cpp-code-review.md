---
layout: post
title: "Cpp Code Review"
date: 2022-11-12
tags: c++ coding development
---

## Rules
* Thou shalt not auto, unless thy faith is strong and pure
* Thou shall not write indexed loops for they are abomination before the code
* Thou shalt wash thy data thoroughly before releasing it
* Thou shalt not accept data from strangers for they might be sinful
* Thou shalt not copy paste thy code blocks
* Thy comparison routines shall be correct or else the wrath of the code will get thee
* Thou shalt not push that which can be emplaced
* Thou shalt search only once
* Thou shalt not cook unsigned values with overflow semantics
* He who is without noexcept shall throw, and none other

## Sensitive memory removal
* Optimized out by compiler!

### Can be fixed by:
* Custom safe_memset + disabled LTO/WPO
* Access a non-volatile object through a volatile pointer
* Call memset through a volatile function pointer
* Volatile assembly code
* Memset + memory barrier
* Disable compiler optimziations (-fno-builtin-memset)
* C11 : memset_s

## Comparison
```cpp
struct Foo {
auto operator<=>(const Foo &rhs) const = default;
};
```

## Reference
* [Hypercritical C++ Code Review - Yuri Minaev](https://www.youtube.com/watch?v=f1_Iwh33f9I)
