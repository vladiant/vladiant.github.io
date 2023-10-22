---
layout: post
title: "C++ Python Interface"
date: 2023-10-22
tags: c++ python design interface performance
---

## Motivation
* Avoid reimplementation of complex code with Python
* Performance
* Back and forth with user's Python code
* Interoperability with data structures in Python - shared memory space

## Tools
* [Python/C API](https://docs.python.org/3/c-api/index.html) - the fastest speed, the smallest library size
* [Cython](https://cython.org/) - New "Python" code / New "C++" code
* [Numba](https://numba.pydata.org/) / [PyPy](https://www.pypy.org/) - Pre-written Python code
* [Boost::Python](https://www.boost.org/doc/libs/1_80_0/libs/python/doc/html/index.html) - Pre-written C++ code. Second best option in terms of size and speed.
* [pybind11](https://pybind11.readthedocs.io/en/stable/basics.html) - Pre-written C++ code
* [cppyy](https://cppyy.readthedocs.io/en/latest/)- New "C++" code

## Basis thought process
* Define user boundary in your library's API
* Expose methods at that boundary using Python binding
* Try putting "hot path" code inside your library
* Can allow Python objects for constructors / non-critical operators

## Functions expose in API
* Init some data structures / load some data
* Configure your class parameters
* Do a lot of complex work inside a "hot loop"
* Fetch internal state of your data structure

## Arguments to functions
* Can be int / float / `std::vector<std::string>`
* Can be instances types defined by your module
* Can be `PyObject*` / `boost::python::object`

## Return values of functions
* Easy enough to return standard types (int , float , ...)
* Can return Python objects - `boost::python::dict`, `boost::python::list`, `boost::python`
* What about larger objects? `boost::python::numpy`

## Lifetime of returned values
* Returned structure `struct1` containing references to another structure `struct2`
* Python will manage `struct1` as a refcounted object
* Python has no way to know that `struct1` refers to `struct2` and will apply garbage collection to `struct2`
* Classic use for shared pointers

## References
* [Writing Python Bindings for C++ Libraries for Performance and Ease of Use - Saksham Sharma - CppNow](https://www.youtube.com/watch?v=2rJJfTt72Dk)
* [Saksham Sharma](https://sakshamsharma.com/)
* <https://github.com/sakshamsharma>
* [Embedding Python in Another Application — Python 3.10.4 documentation](https://docs.python.org/3/extending/embedding.html)

