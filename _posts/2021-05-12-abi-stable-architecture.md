---
layout: post
title: "ABI Stable Architecture"
date: 2021-05-12
---

# Main points
* Export free functions?
* Except the constructor all the functions have the first parameter as pointer of the class
* Export method table instead -> use in [PIMPL](https://en.cppreference.com/w/cpp/language/pimpl)
* Method table shared between components, virtual table remains local
* Method table does not inherit

## Component Interface Binder (CIB)
* [https://github.com/satya-das/cib](https://github.com/satya-das/cib)

## Reference
* [Satya Das - CIB - ABI stable architecture for a C++ SDK](https://www.youtube.com/watch?v=cp-MtGe-f6M)
