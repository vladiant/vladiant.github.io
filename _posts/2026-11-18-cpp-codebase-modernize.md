---
layout: post
title: "C++ Codebase Modernization"
date: 2026-11-18
tags: c++ coding development
---

## Base transformations to modernize legacy code
* For overridden functions, remove the *virtual* keyword and replace with *override*
* Add *const* to member functions and function parameters where appropriate
* Add *noexcept* on member functions that only access class member variables
* Replace unscoped *enums* with *enum class*
* Replace *typedefs* with *using*
* Replace for/while loops over collections with ranged-for
* In ranged-for loops, use structured bindings
* *Inline* Simple Member Functions
* Empty class *constructors/destructors* removed or where *virtual* set to *default*
* Apply use of C++17 style *nested namespace*
* Converting run time *const* variables to *constexpr*
* Initializing class *members* using *Header initialization*
* Remove unused header includes
* Replace *NULL,0* with *nullptr/true/false*
* Apply designated initializers via clang-tidy to all files in tarball
* Apply better container functions
* Replace throw with noexcept
* Replace C standard library headers with their C++ equivalents
* Make trivially-destructible by removing out-of-line defaulted destructor declarations

## Compiler flags
```
-Wall -Wextra -Werror -Wfatal-errors -Wno-comment -Wpedantic -Wrestrict
-Wcast-qual -Wshadow -Wnon-virtual-dtor -Wunused -Wduplicated-cond
-Wcast-align -Wnull-dereference -Wdouble-promotion -Wfloat-equal
-Wuseless-cast -Wsign-conversion -Wconversion -Wno-stringop-overflow
-Wno-array-bounds
```

## Clang Tidy 

### Checks applied to code to modernize it
* modernize-concat-nested-namespaces
* modernize-use-using
* modernize-use-override
* modernize-use-equals-default
* modernize-use-equals-delete
* modernize-use-bool-literals
* modernize-use-nullptr
* modernize-use-default-member-init
* modernize-loop-convert
* modernize-use-noexcept
* modernize-deprecated-headers
* modernize-redundant-void-arg
* readability-container-size-empty
* readability-container-contains
* readability-redundant-member-init
* performance-trivially-destructible

### Observations
* Good results (even with lots of bugs)
* Worked over 2 files max
* Works well with AI writing deterministic fix it scripts
* Residue left over is quite small and manageable
* Cultural comfort with large PRs ( >7500)

### Drawbacks
* Limited amount of checks
* Non-specific

## Tools for static and dynamic code analysis:
* Cppcheck [http://cppcheck.sourceforge.net/](http://cppcheck.sourceforge.net/)
* GCC/G++ warnings [https://gcc.gnu.org/](https://gcc.gnu.org/)
* Visual Studio [https://www.visualstudio.com/](https://www.visualstudio.com/)
* Clang Static Analyzer [https://clang-analyzer.llvm.org/](https://clang-analyzer.llvm.org/)
* Clang-Tidy [http://clang.llvm.org/extra/clang-tidy/](http://clang.llvm.org/extra/clang-tidy/)
* Infer [https://fbinfer.com/](https://fbinfer.com/)
* PC-Lint [http://www.gimpel.com/](http://www.gimpel.com/)
* RATS [https://github.com/andrew-d/rough-auditing-tool-for-security](https://github.com/andrew-d/rough-auditing-tool-for-security)
* Valgrind [http://valgrind.org/](http://valgrind.org/)
* Vera++ [https://bitbucket.org/verateam](https://bitbucket.org/verateam)
* Dr. Memory warnings [http://drmemory.org/](http://drmemory.org/)

## Review
* **Scope Smartly**: Minimize variable scope in conditionals, loops, and switches to boost clarity and reduce bugs.
* **Iterate Elegantly**: Prefer range-based loops, structured bindings, and const& or auto&& for clean and efficient traversal.
* **Design Thoughtfully**: Use enum class, std::variant, std::optional, and std::expected to express intent and avoid ambiguity.
* **Create Classes with Care**: Initialize members early, make functions const or static when appropriate, and use idioms like PassKey and <=> for control and comparison.
* **Modernize with STL**: Embrace std::ranges, erase_if, contains, and emplace_* to replace verbose patterns with expressive, standard solutions.
* Use clang-tidy checks and warnings to help the compiler catch issues.

## References
* [Modernizing Legacy Codebases Without Stopping the World - Peter Muldoon - ACCU on Sea 2026 ](https://www.youtube.com/watch?v=w9k-L0GLLKM)
* [Amir Kirsh - C++ Pitfalls and Sharp Edges to Avoid](https://www.youtube.com/watch?v=xWw8d_Dk4Wo)
* [Back to Basics: How To Improve C++ Code Reviews - Chandranath Bhattacharyya & Kathleen Baker](https://www.youtube.com/watch?v=mMrIwY1n74g)
