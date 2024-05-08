---
layout: post
title: "Shared Libraries Guidelines"
date: 2024-05-08
tags: c++ performance development
---

## Symbol Resolution Time
* [--allow-shlib-undefined](https://manpages.debian.org/jessie/binutils/gold.1.en.html) - Allow unresolved references in shared libraries
* [--no-allow-shlib-undefined](https://manpages.debian.org/jessie/binutils/gold.1.en.html) - Do not allow unresolved references in shared libraries
* [--no-undefined](https://manpages.debian.org/jessie/binutils/gold.1.en.html) - Report undefined symbols

## Easier fallbacks
* [-fvisibility-inlines-hidden](https://gcc.gnu.org/wiki/Visibility) - causes all inlined class member functions to have hidden visibility, causing significant export symbol table size & binary size reductions
* [-fvisibility-ms-compat](https://gcc.gnu.org/onlinedocs/gcc-9.1.0/gcc/C_002b_002b-Dialect-Options.html) - attempts to use visibility settings to make GCC’s C++ linkage model compatible with that of Microsoft Visual Studio.
* [-fno-semantic-interposition](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html) - compiler assumes that if interposition happens for functions the overwriting function will have precisely the same semantics (and side effects). 

## Recommendations for shared libraries on Linux
* Build with [-fvisibility=hidden](https://gcc.gnu.org/onlinedocs/gcc/Code-Gen-Options.html) (every declaration not explicitly marked with a visibility attribute has a hidden visibility) , [-Bsymbolic](https://manpages.debian.org/jessie/binutils/gold.1.en.html) (bind defined symbols locally)
* Mark only exported functions as [_\_attribute\_\_((visibility("protected")))](https://gcc.gnu.org/onlinedocs/gcc-4.1.2/gcc/Function-Attributes.html) (indicates that the symbol will be placed in the dynamic symbol table, but that references within the defining module will bind to the local symbol. The symbol cannot be overridden by another module.)

## Takeaways
* Linux and Windows designs are fundamentally different
* The Linux design is burdened by archaic design goals
* Practical recommendations: [-fvisibility=hidden](https://gcc.gnu.org/onlinedocs/gcc/Code-Gen-Options.html) , [-Bsymbolic](https://manpages.debian.org/jessie/binutils/gold.1.en.html)
* "Shared Libs are outside the scope of the standard" - is not a valid bailout!

## References
* [Linkers, Loaders and Shared Libraries in Windows, Linux, and C++ - Ofek Shilon - CppCon 2023](https://www.youtube.com/watch?v=_enXuIxuNV4)
* <https://github.com/OfekShilon>
* [How to write shared librarires](http://library.bagrintsev.me/CPP/dsohowto.pdf)
* [-fno-semantic-interposition](https://maskray.me/blog/2021-05-09-fno-semantic-interposition)
* [ELF interposition and -Bsymbolic](https://maskray.me/blog/2021-05-16-elf-interposition-and-bsymbolic)
* [Why is the new C++ visibility support so useful?](https://gcc.gnu.org/wiki/Visibility)
* [Declaring Attributes of Functions](https://gcc.gnu.org/onlinedocs/gcc-4.1.2/gcc/Function-Attributes.html)


