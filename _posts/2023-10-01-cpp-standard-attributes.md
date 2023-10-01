---
layout: post
title: "C++ Standard Attributes Studies"
date: 2023-10-01
tags: c++11 c++14 c++17 c++20 c++23 c++
---

## Attributes about warnings
* [deprecated](https://en.cppreference.com/w/cpp/language/attributes/deprecated) - use when needed with string argument what to use instead
* [maybe_unused](https://en.cppreference.com/w/cpp/language/attributes/maybe_unused) - use when needed and consider replacing your existent solutions
* [fallthrough](https://en.cppreference.com/w/cpp/language/attributes/fallthrough) - use when needed
* [nodiscard](https://en.cppreference.com/w/cpp/language/attributes/nodiscard) - use to signal wrong use of the API and add character literal argument

## Attributes about optimisations and undefined behavior
* [noreturn](https://en.cppreference.com/w/cpp/language/attributes/noreturn) - to be used with [std::rethrow_exception](https://en.cppreference.com/w/cpp/error/rethrow_exception), [std::nested_exception::rethrow_nested](https://en.cppreference.com/w/cpp/error/nested_exception/rethrow_nested), [std::throw_with_nested](https://en.cppreference.com/w/cpp/error/throw_with_nested) (always throw), [std::abort](https://en.cppreference.com/w/cpp/utility/program/abort), [std::exit](https://en.cppreference.com/w/cpp/utility/program/exit), [std::quick_exit](https://en.cppreference.com/w/cpp/utility/program/quick_exit), [std::terminate](https://en.cppreference.com/w/cpp/error/terminate) (always terminate the program), [std::longjmp](https://en.cppreference.com/w/cpp/utility/program/longjmp) (always jump), [std::unreachable](https://en.cppreference.com/w/cpp/utility/unreachable) (always undefined behavior). Exper only usage, introduces undefined behavior.
* [carries_dependency](https://en.cppreference.com/w/cpp/language/attributes/carries_dependency) - **never use**
* [likely/unlikely](https://en.cppreference.com/w/cpp/language/attributes/likely) - avoid, use only after improvement is measured, depends on compiler
* [assume](https://en.cppreference.com/w/cpp/language/attributes/assume) - **expert only usage**, conditions should be an invariant to avoid undefined behavior, use only after improvement is measured

## Attributes about ABI
* [no_unique_address](https://en.cppreference.com/w/cpp/language/attributes/no_unique_address) - use if binary size is critical, effects are not reliable or portable

## C attributes
* [deprecated](https://en.cppreference.com/w/cpp/language/attributes/deprecated) - use when needed with string argument what to use instead
* [noreturn](https://en.cppreference.com/w/cpp/language/attributes/noreturn) - to be used with [std::rethrow_exception](https://en.cppreference.com/w/cpp/error/rethrow_exception), [std::nested_exception::rethrow_nested](https://en.cppreference.com/w/cpp/error/nested_exception/rethrow_nested), [std::throw_with_nested](https://en.cppreference.com/w/cpp/error/throw_with_nested) (always throw), [std::abort](https://en.cppreference.com/w/cpp/utility/program/abort), [std::exit](https://en.cppreference.com/w/cpp/utility/program/exit), [std::quick_exit](https://en.cppreference.com/w/cpp/utility/program/quick_exit), [std::terminate](https://en.cppreference.com/w/cpp/error/terminate) (always terminate the program), [std::longjmp](https://en.cppreference.com/w/cpp/utility/program/longjmp) (always jump), [std::unreachable](https://en.cppreference.com/w/cpp/utility/unreachable) (always undefined behavior). Exper only usage, introduces undefined behavior.
* [fallthrough](https://en.cppreference.com/w/cpp/language/attributes/fallthrough) - use when needed
* [nodiscard](https://en.cppreference.com/w/cpp/language/attributes/nodiscard) - use to signal wrong use of the API and add character literal argument
* [maybe_unused](https://en.cppreference.com/w/cpp/language/attributes/maybe_unused) - use when needed and consider replacing your existent solutions
* **reproducible** - equivalent to *gnu::pure* . Effectless (function has no observale side effects) and idempotent (repeated evaluation gives the same result). Assumed and optimised accordingly. If the assumption does not hold undefined behavior happens. Use only if you are sure what you are doing.
* **unsequenced** - equivalent to *gnu::const* . Stateless (function does not define mutable static or thread local objects), effectless, idempotent and independent (does not depend on other state than the argument and constants). Assumed and optimised accordingly. If the assumption does not hold undefined behavior happens. Use only if you are sure what you are doing.

## References
* [Standard Attributes in C and C++ - Timur Doumler - ACCU 2023](https://www.youtube.com/watch?v=TDKqAWtvH9c)
* [C++ attributes](https://en.cppreference.com/w/cpp/language/attributes)
* [C attributes](https://en.cppreference.com/w/c/language/attributes)
* [GNU Common Function Attributes](https://gcc.gnu.org/onlinedocs/gcc/Common-Function-Attributes.html)
