---
layout: post
title: "Most Important C++ Optimizations"
date: 2023-01-12
tags: c++ performance interface
---

## General guidelines
* No unecessary work (copying and allocations)
* Use all computing power (all cores and SIMD)
* Avoid waits and stalls (lockless data structures, job systems, async APIs)
* Use hardware efficiently (cache friendlyness, well predictable code)
* OS level efficiency (OS API)

## 1. Enable compiler optimisations
* Optimize for speed (longer compile time)
   * GCC, LLVM, ICC : -O2 , -O3
   * MSVC : /Ox , /O2
* Optimize for size
   * GCC, LLVM, ICC : -Os
   * MSVC : /O1

## 2. Set target architecture
* x86
   * GCC, LLVM, ICC : -march=native , -mtune=native
   * MSVC : (need to be specified manually) /arch:IA32 , /arch:SSE , /arch:SSE2 , /arch:AVX , /arch:AVX2 , /arch:AVX512

* ARM
   * GCC, LLVM, ICC : -mcpu=native
   * MSVC : (need to be specified manually) /arch:ARMv7VE , /arch:VFPv4 , /arch:armv8.0 ... /arch:armv8.8

## 3. Use fast math (faster computation, less precise results, non-standard compliant)
* GCC, LLVM : -ffast-math (included in -Ofast)
* MSVC : /fp:fast
* ICC : -fp-model=fast

## 4. Disable exceptions and RTTI (limited performqance gains, brekas code using exceptions, non-standard compliant)
* No exceptions
   * GCC, LLVM, ICC : -fno-exceptions
   * MSVC : /EHs-c- /D_HAS_EXCEPTIONS=0
* No RTTI
   * GCC, LLVM, ICC : -fno-rtti
   * MSVC : /GR-

## 5. Enable link time optimization
* GCC, LLVM : -flto
* MSVC : /GL
* ICC : -ipo

## 6. Use unity builds (multiple source files into single source file)
* CMake : -DCMAKE_UNITY_BUILD=ON
* Speeds up compilation

## 7. Link statically
* Static linking
   * Better optimisable
* Dynamic linking
   * More space efficient
   * Can be updated independently of executable

## 8. Use profile guided optimization
* Generate
   * GCC, LLVM : -fprofile-generate
   * MSVC : /GENPROFILE
   * ICC : -prof-gen
* Use
   * GCC, LLVM : -fprofile-use
   * MSVC : /USEPROFILE
   * ICC : -prof-use

## 9. Try different compilers

## 10. Try different standard libraries

## 11. Keep your tools updated

## 12. Preload with a replacement lib
* Linux `env LD_PRELOAD=/usr/lib/.. ./myprogram`

## 13. Use binary post-processing tools

## 14. Constexpr all the things

## 15. Make variables const

## 16. Noexcept all the things

## 17. Use static for internal linkage

## 18. Use [[noreturn]]

## 19. Use [[likely]] and [[unlikely]]

## 20. Use [[assume(condition)]]
* pre C++23
   * GCC : if(!condition) `__builtin_unreachable();`
   * MSVC, ICC : `__assume(condition);`
   * LLVM : `__builtin_assume(condition);`
* Unlike assert it is used for the optimiser and if(!condition) then undefined_behavior

## 21. Use __restrict
* GCC, LLVM, ICC : `__attribute__((malloc))`
* MSVC : `__declspec(restrict)`

## 22. Make functions pure
* GCC, LLVM, ICC : `__attribute__((pure))` or [[gnu::pure]]
* MSVC : Not supported

* GCC, LLVM, ICC : `__attribute__((const))` or [[gnu::const]]
* MSVC : Not supported

## 23. Take parameters properly

## 24. Avoid allocations in loops (move objects out of loops)

## 25. Avoid copying exceptions (catch by reference, rethrow current exception)

## 26. Avoid copies in range-for (of iterated object)

## 27. Avoid copies in lambda captures

## 28. Avoid copies in structured bindings

## 29. Provide ref qualified methods
* (manual hardware oriented optimizations)

## 30. Keep the working set size small

## 31. Exploit data locality
* Prefer continious containers - std::array, std::vector, std::deque, std::flat_map, std::flat_set
* Avoid - std::list, std::set, std::unordered_set, std::map, std::unordered_map
* Iterate in the way data is stored

## 32. Export temporal locality
* Pin thread to a core
   * Linux: pthread_set_affinity
   * Windows: SetThreadAffinityMask
   * macOS: thread_policy_set with thread_affinity_policy_t
* Set priority of the process
   * Linux, macOS: setpriority
   * Windows: SetPriorityClass
* Set priority of a thread
   * Linux: pthread_setschedprio
   * Windows: SetThreadPriority
   * macOS: setThreadPriority

## 33. Avoid false sharing
* Use different cache lines
* alignas(std::hardware_destructive_interference_size)

## 34. Use non temporal stores

## 35. Use indirected calls

## 36. Make branches predictable

## 37. Use branchless optimisations

## 38. Use SIMD intrinsics

## References
* [The Most Important Optimizations to Apply in Your C++ Programs - Jan Bielak - CppCon 2022](https://www.youtube.com/watch?v=qCjEN5XRzHc)
* <https://github.com/janekb04>
