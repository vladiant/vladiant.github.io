---
layout: post
title: "C++ Beware"
date: 2025-10-14
tags: c++ memory performance
---

## Recommendations

### Mind the traps
Be aware of the pifalls, such as Undefined Behaviour, dangling references, slicing, moved-from objects, ...

### Be explicit
Prefer clarity over cleverness, keep your code simple - ambiguity and complexity invite bugs

### Prefer Safer Constructs
RAII, smart pointers, strong typing, constexpr, small functions, stateless vs statefull

### Review and Refactor
Tech debt and legacy code are bug magnets!

### Compiler warnings
* At least `-Wall -Wextra -Werror`
* Recommended: 
```
-Wall -Wextra -Werror -Wfatal-errors -Wno-comment
-Wpedantic -Wrestrict -Wcast-qual -Wshadow -Wnon-virtual-dtor
-Wunused -Wduplicated-cond -Wcast-align
-Wnull-dereference -Wdouble-promotion -Wfloat-equal
-Wuseless-cast -Wsign-conversion -Wconversion
-Wno-stringop-overflow -Wno-array-bounds
```

### Make sure to use the right tools
* Static analyzer tools - enable warnings and try to fix issues found
* Runtime sanitizers - ASan, UBSan, TSan
* Code reviews with real blocking power

### Testing, testing, testing
* Unit testing
* Real meaningful coverage (aim for 100% branch coverage!)
* Fuzz testing
* Integration and System testing

## Reference
* [Amir Kirsh - C++ Pitfalls and Sharp Edges to Avoid](https://www.youtube.com/watch?v=xWw8d_Dk4Wo)
* [GCC Warning Options](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html)

