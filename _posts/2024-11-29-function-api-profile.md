---
layout: post
title: "Function API profiling"
date: 2024-11-29
tags: c++ performance desing
---

## Examples

### Return by value vs output parameter
```
#include <memory>

__attribute__((noinline))
std::unique_ptr<int> value_ptr() {
    return nullptr;
}

__attribute__((noinline))
void output_ptr(std::unique_ptr<int>& dst) {
    dst = nullptr;
}

int* value_ptr_call() {
    auto ptr = value_ptr();
    return ptr.get();
}

int* output_ptr_call() {
    std::unique_ptr<int> ptr;
    output_ptr(ptr);
    return ptr.get();
}

static void return_by_value(benchmark::State& state) {
  for (auto _ : state) {
    benchmark::DoNotOptimize(value_ptr_call());
  }
}
BENCHMARK(return_by_value);

static void output_parameter(benchmark::State& state) {
  for (auto _ : state) {
    benchmark::DoNotOptimize(output_ptr_call());
  }
}
BENCHMARK(output_parameter);

```
* <https://quick-bench.com/q/mOAHh7zZeagJlCJ63GtWVMPngsw>

### Returning a pointer
```
#include <memory>

int* raw_ptr() {
    return nullptr;
}

std::unique_ptr<int> smart_ptr() {
    return nullptr;
}

```
* <https://godbolt.org/z/ExaoKfT1z>

### Return in register vs return in memory
```
#include <memory>

__attribute__((noinline))
int* raw_ptr() {
    return nullptr;
}

__attribute__((noinline))
std::unique_ptr<int> smart_ptr() {
    return nullptr;
}

static void return_in_register(benchmark::State& state) {
  for (auto _ : state) {
    benchmark::DoNotOptimize(raw_ptr());
  }
}
BENCHMARK(return_in_register);

static void return_in_memory(benchmark::State& state) {
  for (auto _ : state) {
    benchmark::DoNotOptimize(smart_ptr());
  }
}
BENCHMARK(return_in_memory);
```
* <https://quick-bench.com/q/pJ3z9L_Q1M16qob8-sg8lM3-T60>

### Wrapper over int
```
https://godbolt.org/z/Tddd4E6hs
```
* <https://godbolt.org/z/Tddd4E6hs>

### Wrapper over int : no custom copy and move
```
struct INT {
    int value;

    INT(int value = 0) : value{value} {}
    ~INT() {}
};

int int_seconds() {
    return 60;
}

INT INT_seconds() {
    return 60;
}

```
* <https://godbolt.org/z/f6s1P96Tx>

### Wrapper over int : no custom constructor
```
struct INT {
    int value = 0;
};

int int_seconds() {
    return 60;
}

INT INT_seconds() {
    return INT{60};
}

```
* <https://godbolt.org/z/c6GbTdjc7>

### std::chrono
```
#include <chrono>

int64_t int_seconds() {
    return 60;
}

std::chrono::seconds chrono_seconds() {
    return std::chrono::seconds{60};
}

static_assert(std::is_same_v<int64_t, std::chrono::seconds::rep>);

```
* <https://godbolt.org/z/E5e1nGY94>

### std::pair and std::tuple
```
#include <utility>
#include <tuple>

int ints_sum(int x, int y) {
    return x + y;
}

int pair_sum(std::pair<int, int> p) {
    return p.first + p.second;
}

int tuple_sum(std::tuple<int, int> t) {
    return std::get<0>(t) + std::get<1>(t);
}

// static_assert(std::is_trivially_copy_constructible_v<std::pair<int, int>>);
// static_assert(std::is_trivially_copyable_v<std::pair<int, int>>);

// static_assert(std::is_trivially_move_constructible_v<std::tuple<int, int>>);
// static_assert(std::is_trivially_copy_constructible_v<std::tuple<int, int>>);
// static_assert(std::is_trivially_destructible_v<std::tuple<int, int>>);

```
* <https://godbolt.org/z/r7McGEb8o>

### RVO : inserting a function result into container
```
#include <optional>

struct large {
    large();
    large(large&&);
    large& operator=(large&&);
    large(large const&);
    large& operator=(large const&);
    ~large();
};
large make_large();

std::optional<large> optional_large() {
    return std::optional<large>{make_large()};
}

```
* <https://godbolt.org/z/bcdsx7aP4>

### Lazy evaluation with ac::lazy
```
#include <optional>

struct large {
    large();
    large(large&&);
    large& operator=(large&&);
    large(large const&);
    large& operator=(large const&);
    ~large();
};
large make_large();

template<class Function>
struct lazy {
    operator std::invoke_result_t<Function>() {
         return function();
    }

    Function function;
};
template<class Function>
lazy(Function&&) -> lazy<Function>;

std::optional<large> lazy_optional_large() {
    return std::optional<large>{lazy{make_large}};
}

```
* <https://godbolt.org/z/PYq6KTPKh>

### Pass by value vs pass by reference
```
#include <memory>

__attribute__((noinline))
bool value_is_zero(int x) {
    return x == 0;
}

__attribute__((noinline))
bool ref_is_zero(int const& x) {
    return x == 0;
}

bool value_is_zero_call() {
    return value_is_zero(1);
}

bool ref_is_zero_call() {
    return ref_is_zero(1);
}

static void pass_by_value(benchmark::State& state) {
  for (auto _ : state) {
    benchmark::DoNotOptimize(value_is_zero_call());
  }
}
BENCHMARK(pass_by_value);

static void pass_by_reference(benchmark::State& state) {
  for (auto _ : state) {
    benchmark::DoNotOptimize(ref_is_zero_call());
  }
}
BENCHMARK(pass_by_reference);
```
* <https://quick-bench.com/q/gVbxyQvoqxN76wfqnWVrFF8kqvQ>

### Int parameter
```
bool value_is_zero(int x) {
    return x == 0;
}

bool ref_is_zero(int const& x) {
    return x == 0;
}
```
* <https://godbolt.org/z/ofznMvKWc>

### Int parameter : extra function
```
bool value_is_zero(int x);
bool ref_is_zero(int const& x);

bool value_is_zero_call() {
    return value_is_zero(1);
}

bool ref_is_zero_call() {
    return ref_is_zero(1);
}
```
* <https://godbolt.org/z/fzshqhd85>


```
void some_extra_function();

bool value_extra_function(int x) {
    int const copy = x;
    some_extra_function();
    return copy == x;
}

bool ref_extra_function(int const& x) {
    int const copy = x;
    some_extra_function();
    return copy == x;
}
```

* <https://godbolt.org/z/4r946xh8T>

### std::mdspan vs raw pointer and sizes
```
#include <cstddef>

int raw_back(int const* ptr, size_t size) {
    return ptr[size - 1];
}

template<class T>
struct Span {
    T* ptr;
    size_t size;
};

int span_back(Span<int const> span) {
    return span.ptr[span.size - 1];
}

//

int raw_back2(int const* ptr, size_t width, size_t height) {
    return ptr[width * height - 1];
}

struct mdspan2 {
    int const* ptr;
    size_t width;
    size_t height;
};

int mdspan_back2(mdspan2 span) {
    return span.ptr[span.width * span.height - 1];
}

```
* <https://godbolt.org/z/bez7c5PMK>
* <https://godbolt.org/z/EcfanMoYf>

### Empty parameter : tag dispatch
```
int raw_rand();

struct mt19937 {};
int tagged_rand(mt19937);

int raw_rand_call() {
    return raw_rand();
}

int tagged_rand_call() {
    return tagged_rand(mt19937{});
}
```
 * <https://godbolt.org/z/vxG4eY1r4>

### Chain of function calls
```
int sum(int x1, int x2);

int sum_12_3(int x1, int x2, int x3) {
    return sum(sum(x1, x2), x3);
}
int sum_13_2(int x1, int x2, int x3) {
    return sum(sum(x1, x3), x2);
}
int sum_23_1(int x1, int x2, int x3) {
    return sum(sum(x2, x3), x1);
}
int sum_21_3(int x1, int x2, int x3) {
    return sum(sum(x2, x1), x3);
}
```
* <https://godbolt.org/z/MsjeT8TTK>

### Copy of a byte span: call site 
```
void raw_copy(std::byte* dst, std::byte const* src, size_t size);
void checked_copy(
    std::byte* dst, std::byte const* src, size_t dst_size, size_t src_size
);
std::array<std::byte, 8> arr;

void raw_copy_call() {
    raw_copy(arr.data(), arr.data(), 8);
}
void checked_copy_call() {
    checked_copy(arr.data(), arr.data(), 8, 8);
}
```
* <https://godbolt.org/z/7M45xz9ha>
* <https://godbolt.org/z/3Tqs849eh>

## Conclusions
* Compilers do unexpected things to your code, because they have to follow all the sepcifications
* Compiler Explorer is your friend: <https://godbolt.org/>
* C++ Core guidelines are pretty reasonable from performance point of view

## Most important guidelines to avoid function call overhead
* Return by value
* Pass "trivial" types by value, others by reference
* Follow the Rule of 0 (or at least support trivial copy)
* Make APIs consistent
* Unerstand abstractions cost of your target paradigm 


## Reference
* [Hidden Overhead of a Function API - Oleksandr Bacherikov - CppCon 2024](https://www.youtube.com/watch?v=PCP3ckEqYK8)




