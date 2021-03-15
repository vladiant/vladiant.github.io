---
layout: post
title: "Non-Blocking Code Notes"
date: 2021-03-15
---

## Guidelines

* Don't swtich between atomic and non-atomic functions
* Target and exploit situations which enforce uniqueness
* Avoid chnaging two things at a time 
  * Sometimes you can exploit bit operations
  * Sometimes intelligent ordering can do the trick
  * Sometimes it is just not possible at all 

## Debugging

* "The instruction pointer game"
* The rules:
  * Pull up two windows (= coroutines) with the same codes
  * You have the instruction pointer that iterates through your code
  * You may switch window at any instruction
  * Watch your variables for race conditions

## Reference

 * Golang UK Conference 2017 Arne Claus - Concurrency Patterns in Go 
 * [Video](https://www.youtube.com/watch?v=rDRa23k70CU)
