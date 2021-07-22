---
layout: post
title: "Practical Go Notes"
date: 2021-06-19
tags: golang design
---

## Guding Principles

1. Simplicity
2. Readability
3. Productivity

## Names
* Short variable names work well when the distance between their declaration and last use is short.
* Long variable names need to justify themselves; the longer they are the more value they need to provide. Lengthy bureaucratic names carry a low amount of signal compared to their weight on the page.
* Don’t include the name of your type in the name of your variable.
* Constants should describe the value they hold, not how that value is used.
* Prefer single letter variables for loops and branches, single words for parameters and return values, multiple words for functions and package level declarations
* Prefer single words for methods, interfaces, and packages.
* Remember that the name of a package is part of the name the caller uses to to refer to it, so make use of that.

## Selected Tips
* If you found yourself with so many nested loops that you exhaust your supply of i, j, and k variables, its probably time to break your function into smaller units.
* If you want to do a renaming across a code-base, do not mix this into another change. If someone is using git bisect they don’t want to wade through thousands of lines of renaming to find the code you changed as well.
* Before you write the function, write the comment describing the function. If you find it hard to write the comment, then it’s a sign that the code you’re about to write is going to be hard to understand.
* Name your package for what it provides, not what it contains.
* Prefer nouns for source file names.
* `main()` should parse flags, open connections to databases, loggers, and such, then hand off execution to a high level object.
* APIs with multiple parameters of the same type are hard to use correctly.
* Give serious consideration to how much time helper functions will save the programmer. Clear is better than concise.
* Avoid exposing APIs with values who only differ in test scope. Instead, use Public wrappers to hide those parameters, use test scoped helpers to set the property in test scope.
* When you find yourself faced with overbearing error handling, try to extract some of the operations into a helper type.

## Site
* [Practical Go: Real world advice for writing maintainable Go programs](https://dave.cheney.net/practical-go/presentations/qcon-china.html)

## Presentation
* [Practical Go: Real World Advice For Writing Maintainable Go Programs](https://www.youtube.com/watch?v=EXrEd1-GZR0)
