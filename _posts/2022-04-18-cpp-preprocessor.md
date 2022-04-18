---
layout: post
title: "C++ Preprocessor Use Or Replace"
date: 2022-04-18
tags: c++ development performance
---

## Format
```cpp
#<directive> <stuff>
```

## Allow command line flags
```bash
g++ test.cpp -DDEBUG_BUILD=true
```
```cpp
if constexpr(DEBUG_BUILD) {
  ...
}
```
Directives do not have scope, the file is processed top down. So moving directives can change generated code.

## Code exclusion antipatterns
* Exclude enum values
* Changing flow control
* Excluding members

## Include
```cpp 
#include <file_to_include>
```
### When to use:
* When you don't have module support
### C alternative:
* None
### C++ alternative
* C++20 modules

## Objects as macros
```cpp 
#define <identifier> <replacement>
#undef <identifier>
```

Reserved:
* start with _
* contain __
* match a language keyword
* match a standardized name

### When to use:
* When you need a value to use during the pre-processing phase
* When you need to support multiple compiler capabilities
* Command line flags
### C alternative:
* For constant expressin use enums
```cpp 
enum {
 ARRAY_SIZE = 44
}
char arr[ARRAY_SIZE]
```
### C++ alternative
* Use constexpr or static const values

## Conditionals
```cpp 
#if <expr>
...
#elif <expr>
...
#else
...
#endif
```

### When to use:
* Include guards
* C linkage specification
```cpp 
#ifndef __cplusplus
 extern C {
#endif
```
* Very sparingly, to exclude code
* Check for header or feature availability flags
### C alternative:
* Attempt to restructure code to limit inline code exclusion
### C++ alternative
* Use constexpr if when all code is available
* Module imports

## Function like macros
```cpp 
#define <identifier>(<arg1>, <arg2>)\
<replacement code>
```
### When to use:
* Perform more complicated pre-processor operations
* Generate blocks of code
### C alternative:
* Create multiple functions for each type with _Generic
### C++ alternative
* constexpr functions
* templates

### Variadic functions like macros
```cpp 
#define <identifier>(<arg1>, ...)\
 <replacement code>
``` 
* Values accessed via [__VA_ARGS__](https://gcc.gnu.org/onlinedocs/cpp/Variadic-Macros.html)
* <stdarg.h> - va_arg, va_start, va_copy, va_end
* GCC: prepend ## to [__VA_ARGS__](https://gcc.gnu.org/onlinedocs/cpp/Variadic-Macros.html) to omit trailing coma in zero arguments case
* C++20: [__VA_OPT__](https://gcc.gnu.org/onlinedocs/cpp/Variadic-Macros.html)

### When to use:
* Perform more complicated pre-processor operations
* Absorb all parameters and turn into noop
### C alternative:
* variadic functions with <stdargs.h>
### C++ alternative
* variadic templates

### Remember:
```cpp 
do {
...
} while(0)
```

## File and line info
* [__LINE__](https://gcc.gnu.org/onlinedocs/cpp/Standard-Predefined-Macros.html)
* [__FILE__](https://gcc.gnu.org/onlinedocs/cpp/Standard-Predefined-Macros.html)
* `#line <next_line_number> <file_name>`

### When to use:
* If you don't have C++20
### C alternative:
* None
### C++ alternative
* C++20 [std::source_location](https://en.cppreference.com/w/cpp/utility/source_location)

## Stringification and Concatenation
```cpp 
#define <identifier>(<text>) #<text>

#define <identifier>(<text1>,<text2>) <text>##<text2>
```

### When to use:
* If you need to generate function or variable names
### C alternative:
* None
### C++ alternative
* Consider templates
* Future: Static ; Reflection/Static ; Generation/Metaclasses

## Pragma
```cpp
#pragma
```
* Inclusion guard
* Warning/error manipulation
* Struct packing (last till he end of current translation unit)

### When to use:
* Limit use as much as possible
### C alternative:
* [__attribute__](https://gcc.gnu.org/onlinedocs/gcc/Variable-Attributes.html)
* [__declspec](https://docs.microsoft.com/en-us/cpp/cpp/declspec?view=msvc-170)
* [__packed__](https://docs.oracle.com/cd/E19205-01/820-7599/giqdb/index.html)
### C++ alternative
* Same as C

## Reference
* [The Preprocessor: Everything You Need to Know and More! - Brian Ruth - CppCon 2021](https://www.youtube.com/watch?v=6KNdGnUiRBM)
