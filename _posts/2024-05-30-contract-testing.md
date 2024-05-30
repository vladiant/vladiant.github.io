---
layout: post
title: "Contract Testing"
date: 2024-05-30
tags: c++ test development
---

## Exception based testing
* `noexcept(true)` and `noexcept(false)`
* `noexcept(sizeof(T) <= SmallObjectsSize)`
* A `true` is used to enable argument that is more performant but would be unsafe in the presence of exceptions
* Wide contract: *no preconditions*
* Narrow contract: *has preconditions*
* When a preconditon is violated - undefined behavior

## Lakos Rule
* We not declare function with a narrow contract noexcept
   - Even if we know it will never throw
   - Instead we document that it does not throw

## Test a precondition check without throwing on failure

### child threads
* Spawn test in child thread
* Assert saves info and locks/freezes thread
* Drawbacks
   - leaks mmeory
   - invalidates RAII
   - leaks one thread per test case
 
### "stackful coroutines"
* Assert fail yields to cooperative scheduler / event loop
* Event look calls next test
* Drawbacks
   - leaks memory
   - invalidates RAII
   - unbounded growth of call stack
   - nontrivial to construct
   - no experience in real world code
 
### Signals
* Just a callback mechanism
* Doesn't solve the problem of leaving function
 
### Fork based death tests
* Launch each test in a forked process
* assert fail terminates process
* Drawbacks
   - requires fast, reliable fork() - UNIX-like systems only!
   - can return only 8 bits of diagnostic data
   - not widely available in unit test frameworks - Gtest only!
 
### Clone based death tests
* More stable than fork-based
* Drawbacks
   - Linux only
 
### Spawn based death tests
* Drawbacks
   - Requires external framework (DejaGNU)
   - Requires moving test into other source file
   - requires buildng state for each test from scratch
   - slow

## Defensive software framework
* Assert-like macroses to check pre/post condition or invariant
* A way to turn checks on and off
* A user settable way to controlwhat happens when a violation is detected

## Possible actions for user-supplied violation handler
* Log the error and continue
* Terminate the program
* Trigger a breakpoint in the debugger
* Executing an endless loop (halt the thread)
* Throw an exception

## Takeaways
* Test your preconditions 
   - Effective to prevent the introduction of bugs across API boundaries due to contract violations

* Best method: Excption-based testing (throw on contract violation)

* Requires that functions with preconditons are not noexcept ("Lakos Rule")

* Only viable alternative to exception based testing: **Death tests** . But:
   - Much more complex
   - Much slower
   - Only works on some specific platforms


## Usable features
* [noexcept specifier](https://en.cppreference.com/w/cpp/language/noexcept_spec)
* [noexcept operator](https://en.cppreference.com/w/cpp/language/noexcept)
* [cassert](https://en.cppreference.com/w/cpp/header/cassert)

## References
* [Noexcept? Enabling Testing of Contract Checks in C++ - Pablo Halpern & Timur Doumler - CppCon 2023](https://www.youtube.com/watch?v=BS3Nr2I32XQ)
* [Ran Regev :: C++26 Contracts](https://www.youtube.com/watch?v=-1syQN5_5D0)
