---
layout: post
title: "Mark Unused Variable"
date: 2021-04-03
---

## Options

1) ```std::ignore = func();``` from ```<tuple>``` header

2) [boost::ignore_unused](https://www.boost.org/doc/libs/1_63_0/libs/core/doc/html/core/ignore_unused.html)

3) ```template <class T> inline void NOTUSED( T const & result ) { static_cast<void>(result); }``` and ```NOTUSED(_client)```

4) According to C++ standard:
```cpp 
void func(int a [[gnu::unused]],
          int b);
```
5) No variable:
```cpp 
void func(int ,
          int b);
```

6) [C++ attribute: maybe_unused](https://en.cppreference.com/w/cpp/language/attributes/maybe_unused) in C++17
