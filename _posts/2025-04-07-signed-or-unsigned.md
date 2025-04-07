---
layout: post
title: "Signed or Unsigned Integer"
date: 2025-04-07
tags: c++ performance
---

## Related C++ Core guidelines
* [ES.100: Don’t mix signed and unsigned arithmetic](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#es100-dont-mix-signed-and-unsigned-arithmetic)
* [ES.101: Use unsigned types for bit manipulation](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#es101-use-unsigned-types-for-bit-manipulation)
* [ES.102: Use signed types for arithmetic](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#es102-use-signed-types-for-arithmetic)

## Operations note
* ADD - 1 cycle
* IMUL - 3 cycles
* DIV - at least 20 times slower then IMUL

## Code samples
```cpp
uint64_t arc_unsigned(uint64_t n) {
   uint64_t sum = 0;
   for(uint64_t i = 1; i <=n; i++) {
      sum += i;
   }
   return sum;
}
```

```cpp
int64_t arc_signed(int64_t n) {
   int64_t sum = 0;
   for(int64_t i = 1; i <=n; i++) {
      sum += i;
   }
   return sum;
}
```

* Undefined behavior in signed utilized in performance improvement in clang-12 ...
* ... and no effect in clang-17

## Recommendations
* Use warning flags `-Wall`, `-Wextra`, `-pedantic`, `-Werror`
* Use newer compilers - they optimize better!
* Use sanitizers - `-fsanitize=signed-integer-oveflow`,`-fsanitize=unsigned-integer-oveflow`
* Use special types for better performance - `int_fastN_t`, `uint_fastN_t`
* Know your CPU
* Use special helpers from the standard - [MAKE_SIGNED](https://en.cppreference.com/w/cpp/types/make_signed), [MAKE_UNSIGNED](https://en.cppreference.com/w/cpp/types/make_unsigned)
* Use [C++20 safe comparators](https://en.cppreference.com/w/cpp/utility/intcmp)
* Avoid using auto when not sure about the type
* Use concrete types when possible!
* Use modern loops as much as you can (instead of indexed ones)
* Use strong types

## Reference
* [To Int or to Uint, This is the Question - Alex Dathskovsky - CppCon 2024](https://www.youtube.com/watch?v=pnaZ0x9Mmm0)
* [UndefinedBehaviorSanitizer](https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html)
* [Fixed width integer types](https://en.cppreference.com/w/cpp/types/integer)
