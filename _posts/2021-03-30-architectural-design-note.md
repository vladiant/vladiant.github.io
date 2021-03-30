---
layout: post
title: "Architectural and design note"
date: 2021-03-30
---

## 1. Each application layer can use low level and own level interfaces for implementing own business logic, but it's a wrong design to use interfaces of upper level.

## 2. Each component shall use only interfaces. Using implementation instead of interface lead to code, linking and other dependencies issues.

## 3. Please, use STL way for working with any data containers. Think twice and look at http://www.cplusplus.com/reference/algorithm/ before implement own loop, search, swap or corporation.

## 4. Avoid using singletons
