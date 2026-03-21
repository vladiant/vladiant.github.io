---
layout: post
title: "C++ Reflection Proposal"
date: 2026-03-21    
tags: c++ c++26 
---

## Herb Sutter's examples
* [Show class members](https://godbolt.org/z/WeaKzWc56)
* [Parse JSON](https://godbolt.org/z/3jzehW1bv)
* [Cmdline Options Parser](https://godbolt.org/z/P6jeKK3of)
* [Ad-hoc polymorphism](https://godbolt.org/z/MEPvEMbqP)
* [Reflection ad-hoc poly T](https://godbolt.org/z/aP4dKfqjo)
* ["interface" metafunction](https://godbolt.org/z/98P4qK36o)
* ["interface" now in EDG](https://godbolt.org/z/7jv9aj8Mh)

## Inbal Levi's examples
* [Basic example](https://godbolt.org/z/WxdvKdcMY)
* [Type info](https://godbolt.org/z/cafxMPo4o)
* [Identifier](https://godbolt.org/z/9YW4bWGM7)
* [Function param names](https://godbolt.org/z/M84Ea6P88)
* [Reflection logger](https://godbolt.org/z/Yddfxdq8j)
* [Reflection library demo](https://godbolt.org/z/dzcbYP4dx)


## Misc C++ Reflection examples

* [Enum](https://godbolt.org/z/W71TqodsW)

```cpp
#include <iostream>
#include <meta>

template <typename E>
struct enum_item {
    std::string_view name;
    E value;
};

template <typename E>
consteval auto get_enum_data() {
    std::array<enum_item<E>, std::meta::enumerators_of(^^E).size()> result;
    int k = 0;
    for (auto mem : std::meta::enumerators_of(^^E))
        result[k++] = enum_item<E>{std::meta::identifier_of(mem),
                                   std::meta::extract<E>(mem)};
    return result;
}

enum class Color { Red, Blue, Green };

int main() {
    std::cout << "members of " << std::meta::identifier_of(^^Color) << '\n';
    for (auto x : get_enum_data<Color>()) {
        std::cout << "  " << x.name << " = " << (long)x.value << '\n';
    }
}
```

* [Simple example](https://godbolt.org/z/bGn95xPvx)
* [Online JSON example - clang experimental P2996](https://godbolt.org/z/7Wvxs6jee)
* [Initial JSON example - clang experimental P2996](https://godbolt.org/z/7Wvxs6jee)
* [EDG GNU Experimental Reflection](https://godbolt.org/z/49cEYePdE)


## References
* [Reflection: C++’s Decade-Defining Rocket Engine - Herb Sutter - CppCon 2025](https://www.youtube.com/watch?v=7z9NNrRDHQU)
* [An Introduction to the new C++ 26 "Reflection" Feature - Inbal Levi - CppCon 2025](https://www.youtube.com/watch?v=HBkG5DpLYo0), [slides](https://slides.com/inballevi/welcome-to-v1-0-of-the-meta-verse-cppcon)
* [C++ 26 Reflections](https://quantdev.blog/posts/reflections/)
* [the hidden compile-time cost of C++26 reflection](https://vittorioromeo.com/index/blog/refl_compiletime.html)
* [C++ Paths and Perspectives, Daveed Vandevoorde / Regularizing C++ for Reflection](https://www.youtube.com/watch?v=uMm4fENHjMc)
* [Discover C++26’s compile-time reflection](https://lemire.me/blog/2025/06/22/c26-will-include-compile-time-reflection-why-should-you-care/)
* <https://github.com/lemire/Code-used-on-Daniel-Lemire-s-blog/blob/master/2025/06/21/sqlinsert.h>
* [Barry's C++ Blog: Reflecting JSON into C++ Objects](https://brevzin.github.io/c++/2025/06/26/json-reflection/)
* [C++26 Reflections adventures & compile time UML](https://www.reachablecode.com/2025/07/31/c26-reflections-adventures-compile-time-uml/)
* [C++26 Reflections adventures & compile time UML](https://www.reachablecode.com/2025/07/31/c26-reflections-adventures-compile-time-uml/)
