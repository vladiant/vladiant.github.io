---
layout: post
title: "Mark Unused Variable"
date: 2021-04-03
tags: c++
---

## Options

1) No variable:
```cpp 
void func(int, int b);
```

2) From ```<tuple>``` header
```cpp
std::ignore = func();
``` 

3) [boost::ignore_unused](https://www.boost.org/doc/libs/1_63_0/libs/core/doc/html/core/ignore_unused.html)

4) ```NOTUSED(_client)``` defined as

```cpp
template <class T>
inline void NOTUSED( T const & result ) { 
   static_cast<void>(result); 
}
``` 

5) According to C++ standard:

```cpp 
void func(int a [[gnu::unused]],
          int b);
```

6) [C++ attribute: maybe_unused](https://en.cppreference.com/w/cpp/language/attributes/maybe_unused) in C++17
