---
layout: post
title: "C++ Reduce Binary Size"
date: 2025-02-12
tags: c++ coding development performance template
---

## Note
* Not everything is a best practice that shaves off a few bytes
* Some things are simply trade-offs

## Heap allocations to shrink your binary?
* Dynamic allocations might keep your binary smaller (but slows down your runtime)
* `std::list` and `std::vector` heap allocates
* C-style containers and `std::array` might be large

## Static storage duration can increase the binary size
* Global and static variables have static storage duration
* Data might end up in the TEXT or DATA segment depending on const ness and initialization
* Local containers won't make huge binaries, even if they are const
* constexpr locals can also take a lot of space!

## Object initialization
* Add something that can be (zero-)initialized at compile-time and only .zerofill will be still used
* Add something that needs runtime initialization and the binary will grow as more code has to be generated

## Member ordering
* Padding is that extra bytes between members
* Alignment requirement is the for memory addresses to start at certain locations
* Order members decreasing order to limit size
* The compiler can often optimize
* It's still a good practice for better cache friendliness and memory footprint

## Special member functions
* Defaults in the header seems to have a big advantage!
* Default implementations differ from empty ones (may be smaller)
* Follow the rule of zero
* Otherwise the rule of five
* And use =default whenever possible!
* On a big project scale, out-of-line defaults shrink the exceutable

## Where to default ?
* In the header, by default
* In the .cpp to avoid inlining and to gain some space

## Not declared move operations might hurt you
* If only copy operations are available, copies will be made
* Even when a move would be more reasonable
* They incur more assembly, so the binary will be bigger
* Follow the rule of 5 if you cannot apply the rule of zero!

## virtual functions
* A single virtual destructor has a big price
* Even if the class is suboptimal for optimization
* Once there is one virtual function, the rest has no big price

## Use minimal templates
* Each template expansion copies code
* The longer the code, the more is copied
* Even though the compiler might optimize
* So keep your template small (both functions and classes)
* And extract the rest
* Use minimal function templates
* Use minimal class templates

## Extern templates
* Limit the number of times code will be generated
* Good for compile time
* Good for binary size
* Put `extern template class Wrapper<int>` in every TU where you instantiate `Wrapper<int>`
* Put `extern template class Wrapper<int>` in the header ( `wrapper.h` ) where you declare `Wrapper<T>`. In `wrapper.cpp` put the explicit template declaration `template class Wrapper<int>;`

## Avoid bloaty class templates
* The more functionalities provide a template the more bloaty it is
* If size is a critical concern for you, think twice before you introduce more
* std / boost etc. types are no exception

## Passing functions around
* Function pointers have an obscure syntax
* `std::function` works out of the box with any kind of lambdas (largest size)
* Templates are quite specializable with concepts
* Go with templates or function pointers when you can

## constexpr functions
* Might be executed at compile-time
* Guarantees no undefined behaviour
* Guarantees implicit inlining
* At least not bigger (optimized)

## Compiler and linker flags
* The simplest one: `-Os`
* Link time optimization: `-flto`
* `-flto=full` / `-fwhole-program` for maximum optimization
* `-fdata-sections` / `-ffunction-sections` (each function or data item into its own section in the output file) and `-Wl,--gc-sections` (dead code elimination)
* `-Wl,--icf=all` or `-Wl,--icf==safe` - Enable identical code folding.
* `-Wl,-s` (omits all symbol information from the output file) and `-Wl,--strip-all` (Do not create .strtab or .symtab.)
* `-Wl,--as-needed` - Normally each link-time shared object has a DT_NEEDED tag. Such a shared object will be loaded by the dynamic loader.
* `-mllvm -inline-threshold=<n>` - how much it should inline functions through 
* `-fstack-protector` - Emit extra code to check for buffer overflows. This makes your binary bigger.

## RTTI
* Turn it off with `-fno-rtti` on gcc/clang, `/GR-` on msvc
* Smaller binary

## Exceptions
* Zero run-time costs
* But the compilation time must be slower
* The binary has to store exception tables and unwind information
* Turn exceptions off - if they are still thrown, `std::terminate` is called.
* Use `noexcept` if you need some exceptions!

## Takeaways
* Care more about compiler and linker settings
* Prevent inlining if size matters - you might not want to default in the header!
* Think twice about exceptions - You might need them but make noexcept whatever you can
* Don't use virtuals in vain
* Consider turning RTTI off
* Think about how you pass around functions

## References
* [How to Keep C++ Binaries Small - Techniques for C++ Optimization - Sandor Dargo - C++ on Sea 2024](https://www.youtube.com/watch?v=7QNtiH5wTAs)
* [Options That Control Optimization](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html)
* [clang - the Clang C, C++, and Objective-C compiler](https://clang.llvm.org/docs/CommandGuide/clang.html)
* [Compilation options](https://gcc.gnu.org/onlinedocs/gnat_ugn/Compilation-options.html)
* [Explain GNU style linker options](https://maskray.me/blog/2020-11-15-explain-gnu-linker-options)
* [Program Library HOWTO](https://dwheeler.com/program-library/Program-Library-HOWTO/x216.html)
* [Clang command line argument reference](https://clang.llvm.org/docs/ClangCommandLineReference.html)
* [Program Instrumentation Options](https://gcc.gnu.org/onlinedocs/gcc/Instrumentation-Options.html)
* [Binary sizes and compiler flags](https://www.sandordargo.com/blog/2023/07/19/binary-sizes-and-compiler-flags)