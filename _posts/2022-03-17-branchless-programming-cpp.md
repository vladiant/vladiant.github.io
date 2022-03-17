---
layout: post
title: "Branchless Programming in C++"
date: 2022-03-17
tags: c++ performance development
---

Profiling
* Google Benchmark <https://github.com/google/benchmark>
* Perf <https://perf.wiki.kernel.org/index.php/Main_Page> 
   * `perf stat`

## Summary
* For best performance use hardware efficiently
* Use all of the hardware all the time (ideal goal)
* Processors can do many computations at once every cycle
* Limiting factor is usually availability of data
* Workaround is pipelining - running multiple instructions streams at once
* Limiting factor is conditional code - next instruction is data dependent
* Workaround is branch prediction - guess the next instruction and go on
* Limiting factor is the ability to guess the future
* Workaround is writing unconditional code with data dependencies

## References
* [Branchless Programming in C++ - Fedor Pikus - CppCon 2021](https://www.youtube.com/watch?v=g-WPhYREFjk)
* https://perfbench.com/
https://quick-bench.com/q/e8QPdYta3Y2BAN0HUnlezkIOJpk

## Code spippets

* Group 1

```cpp
static void BM_branch_predicted(benchmark::State& state) {
  srand(1);
  const unsigned int N = state.range(0);
  std::vector<unsigned long> v1(N), v2(N);
  std::vector<int> c1(N);
  for(size_t i = 0; i < N; i++) {
    v1[i] = rand();
    v2[i] = rand();
    c1[i] = rand()>=0;
  }
  unsigned long* p1 = v1.data();
  unsigned long* p2 = v2.data();
  int* b1 = c1.data();
  for(auto _ : state) {
    unsigned long a1 = 0, a2 = 0;
    for(size_t i = 0; i < N; i++) {
      if(b1[i]) {
        a1 += p1[i];
      } else {
        a2 *= p2[i];
      }
    }
    benchmark::DoNotOptimize(a1);
    benchmark::DoNotOptimize(a2);
    benchmark::ClobberMemory();
  }
  state.SetItemsProcessed(N*state.iterations());
}
// Register the function as a benchmark
BENCHMARK(BM_branch_predicted)->Arg(1<<22);
```

```cpp
static void BM_branch_not_predicted(benchmark::State& state) {
  srand(1);
  const unsigned int N = state.range(0);
  std::vector<unsigned long> v1(N), v2(N);
  std::vector<int> c1(N);
  for(size_t i = 0; i < N; i++) {
    v1[i] = rand();
    v2[i] = rand();
    c1[i] = rand()&0x1;
  }
  unsigned long* p1 = v1.data();
  unsigned long* p2 = v2.data();
  int* b1 = c1.data();
  for(auto _ : state) {
    unsigned long a1 = 0, a2 = 0;
    for(size_t i = 0; i < N; i++) {
      if(b1[i]) {
        a1 += p1[i];
      } else {
        a2 *= p2[i];
      }
    }
    benchmark::DoNotOptimize(a1);
    benchmark::DoNotOptimize(a2);
    benchmark::ClobberMemory();
  }
  state.SetItemsProcessed(N*state.iterations());
}
// Register the function as a benchmark
BENCHMARK(BM_branch_not_predicted)->Arg(1<<22);
```

```cpp
static void BM_branch_predict(benchmark::State& state) {
  srand(1);
  const unsigned int N = state.range(0);
  std::vector<unsigned long> v1(N), v2(N);
  std::vector<int> c1(N);
  for(size_t i = 0; i < N; i++) {
    v1[i] = rand();
    v2[i] = rand();
    if (i==0) c1[i] = rand()>=0; else c1[i] = !c1[i-1];
  }
  unsigned long* p1 = v1.data();
  unsigned long* p2 = v2.data();
  int* b1 = c1.data();
  for(auto _ : state) {
    unsigned long a1 = 0, a2 = 0;
    for(size_t i = 0; i < N; i++) {
      if(b1[i]) {
        a1 += p1[i];
      } else {
        a2 *= p2[i];
      }
    }
    benchmark::DoNotOptimize(a1);
    benchmark::DoNotOptimize(a2);
    benchmark::ClobberMemory();
  }
  state.SetItemsProcessed(N*state.iterations());
}
// Register the function as a benchmark
BENCHMARK(BM_branch_predict)->Arg(1<<22);
```

* Group 2

```cpp
static void BM_false_branch(benchmark::State& state) {
  srand(1);
  const unsigned int N = state.range(0);
  std::vector<unsigned long> v1(N), v2(N);
  std::vector<int> c1(N), c2(N);
  for(size_t i = 0; i < N; i++) {
    v1[i] = rand();
    v2[i] = rand();
    c1[i] = rand()&0x1;
    c2[i] = !c1[i];
  }
  unsigned long* p1 = v1.data();
  unsigned long* p2 = v2.data();
  int* b1 = c1.data();
  int* b2 = c2.data();
  for(auto _ : state) {
    unsigned long a1 = 0, a2 = 0;
    for(size_t i = 0; i < N; i++) {
      if(b1[i] || b2[i]) {
        a1 += p1[i];
      } else {
        a2 *= p2[i];
      }
    }
    benchmark::DoNotOptimize(a1);
    benchmark::DoNotOptimize(a2);
    benchmark::ClobberMemory();
  }
  state.SetItemsProcessed(N*state.iterations());
}
// Register the function as a benchmark
BENCHMARK(BM_false_branch)->Arg(1<<22);
```

```cpp
static void BM_false_branch2(benchmark::State& state) {
  srand(1);
  const unsigned int N = state.range(0);
  std::vector<unsigned long> v1(N), v2(N);
  std::vector<int> c1(N), c2(N);
  for(size_t i = 0; i < N; i++) {
    v1[i] = rand();
    v2[i] = rand();
    c1[i] = rand()&0x1;
    c2[i] = !c1[i];
  }
  unsigned long* p1 = v1.data();
  unsigned long* p2 = v2.data();
  int* b1 = c1.data();
  int* b2 = c2.data();
  for(auto _ : state) {
    unsigned long a1 = 0, a2 = 0;
    for(size_t i = 0; i < N; i++) {
      if(bool(b1[i]) + bool(b2[i])) {
        a1 += p1[i];
      } else {
        a2 *= p2[i];
      }
    }
    benchmark::DoNotOptimize(a1);
    benchmark::DoNotOptimize(a2);
    benchmark::ClobberMemory();
  }
  state.SetItemsProcessed(N*state.iterations());
}
// Register the function as a benchmark
BENCHMARK(BM_false_branch2)->Arg(1<<22);
```

* Group 3

```cpp
static void BM_branched(benchmark::State& state) {
  srand(1);
  const unsigned int N = state.range(0);
  std::vector<unsigned long> v1(N), v2(N);
  std::vector<int> c1(N);
  for(size_t i = 0; i < N; i++) {
    v1[i] = rand();
    v2[i] = rand();
    c1[i] = rand()&0x1;
  }
  unsigned long* p1 = v1.data();
  unsigned long* p2 = v2.data();
  int* b1 = c1.data();
  for(auto _ : state) {
    unsigned long a1 = 0, a2 = 0;
    for(size_t i = 0; i < N; i++) {
      if(b1[i]) {
        a1 += p1[i];
      } else {
        a2 *= p2[i];
      }
    }
    benchmark::DoNotOptimize(a1);
    benchmark::DoNotOptimize(a2);
    benchmark::ClobberMemory();
  }
  state.SetItemsProcessed(N*state.iterations());
}
// Register the function as a benchmark
BENCHMARK(BM_branched)->Arg(1<<22);
```

```cpp
static void BM_branchless(benchmark::State& state) {
  srand(1);
  const unsigned int N = state.range(0);
  std::vector<unsigned long> v1(N), v2(N);
  std::vector<int> c1(N);
  for(size_t i = 0; i < N; i++) {
    v1[i] = rand();
    v2[i] = rand();
    c1[i] = rand()&0x1;
  }
  unsigned long* p1 = v1.data();
  unsigned long* p2 = v2.data();
  int* b1 = c1.data();
  for(auto _ : state) {
    unsigned long a1 = 0, a2 = 0;
    for(size_t i = 0; i < N; i++) {
      unsigned long s1[2] = {0, p1[i] - p2[i]};
      unsigned long s2[2] = {p1[i] * p2[i], 0};
      a1 += s1[bool(b1[i])];
      a2 += s2[bool(b1[i])];
    }
    benchmark::DoNotOptimize(a1);
    benchmark::DoNotOptimize(a2);
    benchmark::ClobberMemory();
  }
  state.SetItemsProcessed(N*state.iterations());
}
// Register the function as a benchmark
BENCHMARK(BM_branchless)->Arg(1<<22);
```
