---
layout: post
title: "Programminng Prompts"
date: 2026-03-16    
tags: ai
---

## Guidelines
* Use a role model
* Add examples
* Always provide context
* Determine the style of your answer
* Look for detailed step-by-step explanations

## Surgeon-Architect
Deep refactoring
```
### Instructions ###
You are a FAANG-level Staff Software Engineer with 15 years of backend experience.
Your task is to ruthlessly refactor the Python code below (written in FastAPI).

Problem: This code is a typical "all-knowing object" and violates SOLID principles.
The route processes database requests directly via SQLAlchemy, implements business logic within the router, sends an email, and returns a response.

What you need to do:
1. Divide this code into three layers: router, service (business logic), and repository (data access).
2. Use dependency injection (DI).
3. Add Pydantic schemas for input and output data to ensure typing.
4. Be sure to use asynchronous database sessions.

Return only the updated code.

### Code for refactoring ###
```

## Patient Mentor
Parsing incomprehensible code
```
### Role and Task ###
You are a mentor, a technically savvy Senior Frontend Developer. I am a Junior Developer.
Please explain this piece of TypeScript code to me so that I fully understand what it does under the hood.

Answer Requirements:
1. Start with a brief summary (in two sentences) – what is the overall purpose of the function?
2. Provide a step-by-step walkthrough of the function's logic.
3. Explain what happens in edge cases: for example, if the input is null, an empty array, or an object without the required keys.
4. If the code is poorly written, suggest a more readable, modern version (for example, avoiding unnecessary reduce statements when map/filter or optional chaining can be used?).

### Code to analyze ###
```

## QA-paranoid
Generating impenetrable tests
```
### Instructions ###
Act like a paranoid QA Automation Engineer who loves finding bugs and ensuring 100% code test coverage.
I use the Vitest framework and the React Testing Library (@testing-library/react).

Write a comprehensive set of unit tests for the following React component.

Your tests should:
1. Strictly follow the arrange-act-assert (AAA) pattern with comments for each step.
2. Cover not only the "happy path" (successful scenarios) but also edge cases:
- What if the API returns a 500 error?
- What if the user quickly clicks the button twice?
- Check that the button becomes disabled during loading.
3. Mock the global fetch API (using Vitest's built-in tools) and clear the mocks after each test (afterEach).

Emit only the test code.

### Component ###
```

## Polyglot translator
Code migration and translations
```
### Instructions ###
Your task is to convert (migrate) old PHP code to modern Python (version 3.11+).

Migration Rules:
1. Preserve the original business logic 1:1. Don't remove functionality!
2. Use modern Python features: typing (type hints), `dataclasses` (if data classes are needed), f-strings.
3. Remove all PHP-specific dirty hacks (like strange array manipulations) and use standard Python approaches (e.g., list comprehensions or dictionary comprehensions).
4. Add Google-format docstrings for all created functions.
5. Write a brief explanation of which Python standard library functions replaced built-in PHP functions (e.g., how you handled working with dates or arrays).

### PHP Code ###
```

## Cruel reviewer
Code review and security audit
```
### Instructions ###
Act as a ruthless Staff Security Engineer / Senior Reviewer in Go. Your task is to conduct a rigorous code review and security audit of the provided snippet.

Look for the following issues:
- Race conditions.
- Goroutine leaks / memory leaks.
- Security vulnerabilities (path traversal, SQLi, etc.).
- Poor error handling.

Response format:
Print a Markdown table with the following columns: Vulnerability/Issue | Severity | Explanation.
After the table, suggest a corrected version of the code (only the corrected code, no unnecessary fluff).

Be extremely critical; do not praise the code.

### Code for audit (vulnerable Go server) ###
```

## Database Talker
SQL optimization
```
### Instruction ###
You are a Senior Database Administrator (DBA) specializing in PostgreSQL.
This SQL query is catastrophically slow. The 'orders' table contains 10 million rows, and the 'users' table contains 2 million.

Below is:
1. The problematic query itself.
2. The query execution plan (EXPLAIN ANALYZE) produced by the database.

Your task:
1. Analyze the EXPLAIN ANALYZE output and pinpoint the exact bottleneck, such as a seq scan, nested loop, or in-memory sort.
2. Rewrite the SQL query for maximum optimization (use CTEs, window functions, or JOINs if subqueries are slow).
3. Suggest 'CREATE INDEX' commands that will fully cover this query (use composite or partial indexes, if necessary).

### Slow SQL Query ###
```

## Refactoring
```
Perform a refactoring of the following "spaghetti code" in DataProcessor.java. Requirements:

1. Break down the monolithic method into logical classes with proper separation of concerns (e.g., a separate class for calculations, another for data processing).
2. Add error handling (use exceptions instead of printing to console).
3. Write Javadoc for each new class and method.
4. Briefly explain the architectural changes you made and why.
```

## Checklist
* Can we explain why we use AI, not just how?
* Do we know when AI should not be used?
* Is it improving quality, not just speed?
* Do we have common practices, not individual experiments?

## References
* [Как правилно да задавате заявки към ChatGPT: 5 прости правила](https://www.kaldata.com/it-%d0%bd%d0%be%d0%b2%d0%b8%d0%bd%d0%b8/%d0%ba%d0%b0%d0%ba-%d0%bf%d1%80%d0%b0%d0%b2%d0%b8%d0%bb%d0%bd%d0%be-%d0%b4%d0%b0-%d0%b7%d0%b0%d0%b4%d0%b0%d0%b2%d0%b0%d1%82%d0%b5-%d0%b7%d0%b0%d1%8f%d0%b2%d0%ba%d0%b8-%d0%ba%d1%8a%d0%bc-chatgpt-5-657636.htm)
* [Лучшие промпты для генерации кода и программистов](https://habr.com/ru/companies/bothub/articles/1017096/)
* [Пробуем использовать бесплатные ИИ для написания кода](https://habr.com/ru/articles/1019326/)
* [AI инструменти ≠ AI умения: къде се чупят нещата](https://dev.bg/digest/ai-tools-ai-skills-sirma-dc03/)

