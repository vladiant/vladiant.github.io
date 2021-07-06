---
layout: post
title: "Naming Is Hard"
date: 2021-07-01
---

## Names exist outside your code
*  Headings on reports
* Emails
* Prompts
* Human conversations about the system

## Use the same words/names in all contexts
* Everyone should call things by their proper names, everywhere

## Don’t use the same words for different things
* Be arbitrary: a certification expires but a coupon becomes invalid
* Then stick to it

## Don’t Invent Business Words 
* Naming pieces of a function is hard
* Avoid pre/post and other “dependent” names
* Unless the business uses them
* Prefer single English words like Save or Location to implementation-focused words like UpdateConfigFile or StorageCoOrdinates

## Don’t Mismatch Natural Pairs
* Begin goes with end, not last (last goes with first)
* Create goes with destroy, not cleanup
* Open goes with close, not release
* Next goes with previous, not rewind
* Put goes with get, not retrieve
* Source goes with destination, not target

## Some Heuristics for Functions
* Verbs Help Functions Make Sense
* Order Matters
* Tools Matter
  * If similar functions all start the same
  * They are listed together in IDEs that show alphabetical lists of functions
  * They may be sorted together by tidiers that do so
  * You may have to type more of them before you can autocomplete
* Parameters
  * They are local variables in the function scope, so you name them with that in mind
  * Never shadow member variables, but please also don’t argx
  * They are cues to the function caller - Never omit them in headers

## Classes Are Nouns
* Anything ending in er (et al) is suspect without a noun
* Don’t overdecorate - Prefixes such as project names are clutter
* Don’t list the contents

## Traditional Member Function Names
* If you put real work in a constructor or a destructor, others will know when it happens
* We recognize get/set for better or worse

## Some Heuristics for Local Variables
* Rarely, Shorter is Better
* Most of the Time, Longer is Better
* Focus on the purpose of the variable, not what it holds
* Consider the greppers
* Abbreviations are generally bad

## Some Heuristics for Templates
* If you write a templated function, it’s a function, so use those approaches
* If you write a templated class, it’s a class, so use those approaches
* Typename Names: 
  *  Only one? T 
  *  Two? Please be meaningful

## Better Naming
* Care about the code you write, and the people who will read it
* Think about the purposes functions, classes etc serve and how they are used
* Don’t be paralyzed by being unable to name something at first
* Demand good names from yourself and those around you
* When you learn what something is, fix its name
* When you change what something is, change its name
* Use consistency and story telling to guide your choices

## Reference
* [Naming is Hard: Let's Do Better - Kate Gregory](https://www.youtube.com/watch?v=ZDluHz-ybPE)
