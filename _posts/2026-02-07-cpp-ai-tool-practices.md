---
layout: post
title: "C++ AI Tools Best Practices"
date: 2026-02-07
tags: ai c++
---

## 1. Properly Set Up Your Environment
* Warnings
* Static Analysis
* Dynamic Analysis
* Exhaustive Tests
* Follow well accepted practices
* `-Wall -Wextra -Wconversion -Wshadow`. `/W4`
* Clang-tidy integration
* Undefined behavior and address sanitizers
* Default warnings as errors
* `--coverage` and single step to run test/coverage results
* Error if tools cannot be found during the configuration
* Use `make` commands and document them in ReadMe

## 2. Don't fully trust the bot (don't vibe)
* Every PR Must Be Reviewed Like It's From Someone on the Internet

## 3. More than autocomplete, less than vibing

## 4. Be Aware Of Context Limitations

## 5. Think Of The Bot As Your Intern With A Short Attention Span
* Has read the entire Internet
* Can work an order of magnitude faster than you can
* Will get distracted and start working on tangentally related things
* Will get stuck in one way of doing things (not necessarily the way you want)

## 6. Have Startup Instructions And Directives Written Out
* Each time your AI bot restarts, it's like having to get a brand new developer up to speed on the project
* Provide a set of instructionsin a well defined place that explain:
   * How to compile
   * Tools in use
   * Coding standards that cannot be enforced with tooling
* Keep this file succint: You don't want to overload the context of the LLM (just like you don't want to with a human!)

## 7. Avoid Negative Directives
* Like with humans
* Avoid saying "never do X" or "don't forget to do Y"
* Instead say "always do W" and "remember to do Z"

## 8. Avoid vague or broad directives
* No "Use modern C++" - "write constexpr enabled C++20 that has constexpr testing for all features"

## 9. Always Remove Stale Code and Stale Files
* Don't let it comment out code or put in negative comments

## 10. Achieve close to 100% code coverage before you do any refactoring or adding
* You are allowed to have it create the test framework
* Establish at least some tests that have the look and feel you want (the bot fill follow your patterns)
* Tell the bot to use coverage to guide the new tests - aim for 100% test coverage
* The bot is likely to write tests that match current behavior
* Have it generate a list of mismatches between expected behavior and current behavior

## 11. Work From A Task List
* Probably most simple if this is a local markdown file
* It can be driven by your issue tracker
* Your first task need to be those that were marked as mismatches during creation of the tests
* The bot itself can help you create the task list

## Work With The Bot
* Your first task should be to go through failing or questionable tests
* Pick a task to complete
* Have it ask you clarifying questions
* Have it perform the task
* Have it create (or update) the tests
* Verify it correctly ran all tests, all analysis, all code formatting
* Verify code coverage did not decrease
* Verify it did not disable any tools or tests
* Have it create a commit

## 12. Verify Its Work
* Remember: They will work around your rules
* Remember: They will forget to verify things you care about

## Saves Time
* Tests uncovered corner cases previously hadn't considered
* Dozens of bugs were discovered and fixed much faster

## 13. Be Willing To Move On If It's Not Able To Help With A Certain Task

## Reference
* [Best Practices for AI Tool Use in C++ - Jason Turner - CppCon 2025](https://www.youtube.com/watch?v=xCuRUjxT5L8)
