---
layout: post
title: "Best Generated AI Code"
date: 2026-06-02    
tags: c++ development ai
---

## Guidelines
* Have one distinct task to complete
* Very clear goal
* The task should be repeatable
* Use a sandbox mode to prevent the bot from "escaping"
* Give the AI a good mode to follow - it will amplify decisions in your code!

## Claude
* Inspect the generated code - always!
```
/init
Add some C++ best practices to follow in the CLAUDE.md
Pretend like you are Jason Turner, and update the CLAUDE.md file with a list of Best Practices for C++
Add rules for variable naming and style
Update the code to follow best practices
```
* Be careful with instructions "No", "Never" and similar. Just show what should be done!
* Conisder replacing `gcc` with `<compiler>`
* Add specific flags - `-g -Wall -Wextra -Wshadow` or `-O3 -Wall -Wextra -Wshadow`
* Add `compile with both clang and gcc`
* Provide example as inline code

```
Update test.cpp to follow best practices and compile and test it
```

## References
* [C++ Weekly - Ep 535 - Getting The Best AI Generated Code](https://www.youtube.com/watch?v=NtbQ-mF3iJE)


