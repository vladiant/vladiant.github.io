---
layout: post
title: "Programming AI Prompts"
date: 2026-03-09
tags: ai c++ python
---

## Guidelines
* Agent errors are your responsibility
* Context is fuel
* Never start implementation without an approved plan.
* Acceptance: Tests instead of Code Review
* Verification: Checking with Reality
* Git Hygiene: Save!

## Planning

### Autonomy

The agent must include in the plan everything required for its implementation:
* point out any subtleties;
* reference project standards/norms/rules;
* take into account the correct interaction of subsystems;
* use project dependencies;
* avoid overengineering;
* solve problems in the simplest possible way while maintaining full functionality.

### Closing Gaps

Once the plan is formed, ask the agent to:
* recheck it;
* add any omitted information;
* clarify and ask questions on any unclear topics;
* close any remaining gaps.

Only when the agent has no questions can the plan be considered finalized.
Always create a final, complete version of the plan as a single text.

### Commitment

Always save the original plan as an .md file so that it can be used as a reference.
Even if your agent is highly skilled at managing context (like the Codex CLI), this is still an absolutely necessary step.

### Implementing the plan is the easiest thing!

Ask the agent to complete the plan's steps and guide them through its full implementation.

## Prompts

### Converting code between languages
```
Transform a Python code fragment into a JavaScript equivalent, preserving the same logic and functionality. Use idiomatic JavaScript syntax and modern language constructs.
```

### Refactoring for readability and style
```
Refactor this code to improve readability and maintainability.
```

### Replacing the for loop with list comprehension
```
Rewrite this Python code using list comprehension.

```

### Switching to smart pointers in C++
```
Rewrite the code in C++, replacing raw pointers and new/delete with std::unique_ptr.
```

### Function documentation in Python
```
Generate a docstring for this function in Google or NumPy format describing the parameters and return value.
```

### C++: Modern Syntax (Auto and Range-Based For)
```
Update this C++ code to use auto and range-based for where appropriate.
```


### References
* [6 советов от практиков AI coding](https://habr.com/ru/articles/997098/)
* [ChatGPT 5.2](https://chatgpt.com/)
* [Готовые промпты для программистов: шаблоны под Python, JavaScript и C++](https://habr.com/ru/companies/bothub/articles/989304/)
