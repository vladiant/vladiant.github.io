---
layout: post
title: "Simple Makefile Guide"
date: 2021-03-21
---

## What is Make? And Why Should I Care?

The tool called [Make](http://en.wikipedia.org/wiki/Make_%28software%29) is a build dependency manager. That is, it takes care of knowing what commands need to be executed in what order to take your software project from a collection of source files, object files, libraries, headers, etc., etc.---some of which may have changed recently---and turning them into a correct up-to-date version of the program.

Actually, you can use Make for other things too, but I'm not going to talk about that.

## A Trivial Makefile

Suppose that you have a directory containing: `tool` `tool.cc` `tool.o` `support.cc` `support.hh`, and `support.o` which depend on `root` and are supposed to be compiled into a program called `tool`, and suppose that you've been hacking on the source files (which means the existing `tool` is now out of date) and want to compile the program.

To do this yourself you could

1. Check if either support.cc or support.hh is newer than support.o, and if so run a command like

```
g++ -g -c -pthread -I/sw/include/root support.cc
```

2. Check if either support.hh or tool.cc are newer than tool.o, and if so run a command like

```
g++ -g  -c -pthread -I/sw/include/root tool.cc
```

3. Check if tool.o is newer than tool, and if so run a command like

```
g++ -g tool.o support.o -L/sw/lib/root -lCore -lCint -lRIO -lNet -lHist -lGraf -lGraf3d -lGpad -lTree -lRint \
-lPostscript -lMatrix -lPhysics -lMathCore -lThread -lz -L/sw/lib -lfreetype -lz -Wl,-framework,CoreServices \
-Wl,-framework,ApplicationServices -pthread -Wl,-rpath,/sw/lib/root -lm -ldl
```

Phew! What a hassle! There is a lot to remember and several chances to make mistakes. (BTW-- the particulars of the command lines exhibited here depend on our software environment. These ones work on my computer.)

Of course, you could just run all three commands every time. That would work, but it doesn't scale well to a substantial piece of software (like DOGS which takes more than 15 minutes to compile from the ground up on my MacBook).

Instead you could write a file called `makefile` like this:

```
tool: tool.o support.o
    g++ -g -o tool tool.o support.o -L/sw/lib/root -lCore -lCint -lRIO -lNet -lHist -lGraf -lGraf3d -lGpad -lTree -lRint \
        -lPostscript -lMatrix -lPhysics -lMathCore -lThread -lz -L/sw/lib -lfreetype -lz -Wl,-framework,CoreServices \
        -Wl,-framework,ApplicationServices -pthread -Wl,-rpath,/sw/lib/root -lm -ldl

tool.o: tool.cc support.hh
    g++ -g  -c -pthread -I/sw/include/root tool.cc

support.o: support.hh support.cc
    g++ -g -c -pthread -I/sw/include/root support.cc
```

and just type `make` at the command line. Which will perform the three steps shown above automatically.

The unindented lines here have the form _"target: dependencies"_ and tell Make that the associated commands (indented lines) should be run if any of the dependencies are newer than the target. That is, the dependency lines describe the logic of what needs to be rebuilt to accommodate changes in various files. If `support.cc` changes that means that `support.o` must be rebuilt, but `tool.o` can be left alone. When `support.o` changes `tool` must be rebuilt.

The commands associated with each dependency line are set off with a tab (see below) should modify the target (or at least touch it to update the modification time).

## Variables, Built In Rules, and Other Goodies

At this point, our makefile is simply remembering the work that needs doing, but we still had to figure out and type each and every needed command in its entirety. It does not have to be that way: Make is a powerful language with variables, text manipulation functions, and a whole slew of built-in rules which can make this much easier for us.

### Make Variables

The syntax for accessing a make variable is `$(VAR)`.

The syntax for assigning to a Make variable is: `VAR = A text value of some kind` (or `VAR := A different text value but ignore this for the moment`).

You can use variables in rules like this improved version of our makefile:

```
CPPFLAGS=-g -pthread -I/sw/include/root
LDFLAGS=-g
LDLIBS=-L/sw/lib/root -lCore -lCint -lRIO -lNet -lHist -lGraf -lGraf3d -lGpad -lTree -lRint \
       -lPostscript -lMatrix -lPhysics -lMathCore -lThread -lz -L/sw/lib -lfreetype -lz \
       -Wl,-framework,CoreServices -Wl,-framework,ApplicationServices -pthread -Wl,-rpath,/sw/lib/root \
       -lm -ldl

tool: tool.o support.o
    g++ $(LDFLAGS) -o tool tool.o support.o $(LDLIBS)

tool.o: tool.cc support.hh
    g++ $(CPPFLAGS) -c tool.cc

support.o: support.hh support.cc
    g++ $(CPPFLAGS) -c support.cc
```

which is a little more readable, but still requires a lot of typing.

### Make Functions

GNU make supports a variety of functions for accessing information from the filesystem or other commands on the system. In this case we are interested in `$(shell ...)` which expands to the output of the argument(s), and `$(subst opat,npat,text)` which replaces all instances of `opat` with `npat` in text.

Taking advantage of this gives us:

```
CPPFLAGS=-g $(shell root-config --cflags)
LDFLAGS=-g $(shell root-config --ldflags)
LDLIBS=$(shell root-config --libs)

SRCS=tool.cc support.cc
OBJS=$(subst .cc,.o,$(SRCS))

tool: $(OBJS)
    g++ $(LDFLAGS) -o tool $(OBJS) $(LDLIBS)

tool.o: tool.cc support.hh
    g++ $(CPPFLAGS) -c tool.cc

support.o: support.hh support.cc
    g++ $(CPPFLAGS) -c support.cc
```

which is easier to type and much more readable.

Notice that

1. We are still stating explicitly the dependencies for each object file and the final executable
2. We've had to explicitly type the compilation rule for both source files

### Implicit and Pattern Rules

We would generally expect that all C++ source files should be treated the same way, and Make provides three ways to state this:

1. suffix rules (considered obsolete in GNU make, but kept for backwards compatibility)
2. implicit rules
3. pattern rules

Implicit rules are built in, and a few will be discussed below. Pattern rules are specified in a form like

```
%.o: %.c
    $(CC) $(CFLAGS) $(CPPFLAGS) -c $<
```

which means that object files are generated from C source files by running the command shown, where the "automatic" variable `$<` expands to the name of the first dependency.

### Built-in Rules

Make has a whole host of built-in rules that mean that very often, a project can be compile by a very simple makefile, indeed.

The GNU make built in rule for C source files is the one exhibited above. Similarly we create object files from C++ source files with a rule like `$(CXX) -c $(CPPFLAGS) $(CFLAGS)`.

Single object files are linked using `$(LD) $(LDFLAGS) n.o $(LOADLIBES) $(LDLIBS)`, but this won't work in our case, because we want to link multiple object files.

### Variables Used By Built-in Rules

The built-in rules use a set of standard variables that allow you to specify local environment information (like where to find the ROOT include files) without re-writing all the rules. The ones most likely to be interesting to us are:

* `CC` -- the C compiler to use
* `CXX` -- the C++ compiler to use
* `LD` -- the linker to use
* `CFLAGS` -- compilation flag for C source files
* `CXXFLAGS` -- compilation flags for C++ source files
* `CPPFLAGS` -- flags for the c-preprocessor (typically include file paths and symbols defined on the command line), used by C and C++
* `LDFLAGS` -- linker flags
* `LDLIBS` -- libraries to link

## A Basic Makefile

By taking advantage of the built-in rules we can simplify our makefile to:

```
CC=gcc
CXX=g++
RM=rm -f
CPPFLAGS=-g $(shell root-config --cflags)
LDFLAGS=-g $(shell root-config --ldflags)
LDLIBS=$(shell root-config --libs)

SRCS=tool.cc support.cc
OBJS=$(subst .cc,.o,$(SRCS))

all: tool

tool: $(OBJS)
    $(CXX) $(LDFLAGS) -o tool $(OBJS) $(LDLIBS)

tool.o: tool.cc support.hh

support.o: support.hh support.cc

clean:
    $(RM) $(OBJS)

distclean: clean
    $(RM) tool
```

We have also added several standard targets that perform special actions (like cleaning up the source directory).

Note that when make is invoked without an argument, it uses the first target found in the file (in this case all), but you can also name the target to get which is what makes make clean remove the object files in this case.

We still have all the dependencies hard-coded.

## Some Mysterious Improvements

```
CC=gcc
CXX=g++
RM=rm -f
CPPFLAGS=-g $(shell root-config --cflags)
LDFLAGS=-g $(shell root-config --ldflags)
LDLIBS=$(shell root-config --libs)

SRCS=tool.cc support.cc
OBJS=$(subst .cc,.o,$(SRCS))

all: tool

tool: $(OBJS)
    $(CXX) $(LDFLAGS) -o tool $(OBJS) $(LDLIBS)

depend: .depend

.depend: $(SRCS)
    $(RM) ./.depend
    $(CXX) $(CPPFLAGS) -MM $^>>./.depend;

clean:
    $(RM) $(OBJS)

distclean: clean
    $(RM) *~ .depend

include .depend
```

Notice that

1. There are no longer any dependency lines for the source files!?!
2. There is some strange magic related to .depend and depend
3. If you do `make` then `ls -A` you see a file named `.depend` which contains things that look like make dependency lines

## Other Reading

* [GNU make manual](http://www.gnu.org/software/make/manual/make.html)
* [Recursive Make Considered Harmful](http://miller.emu.id.au/pmiller/books/rmch/) on a common way of writing makefiles that is less than optimal, and how to avoid it.

## Know Bugs and Historical Notes

The input language for Make is whitespace sensitive. In particular, _the action lines following dependencies must start with a tab_. But a series of spaces can look the same (and indeed there are editors that will silently convert tabs to spaces or vice versa), which results in a Make file that looks right and still doesn't work. This was identified as a bug early on, but ( [the story goes](http://www.catb.org/esr/writings/taoup/html/ch15s04.html) ) it was not fixed, because there were already 10 users.

## Reference
* [https://stackoverflow.com/questions/2481269/how-to-make-a-simple-c-makefile](https://stackoverflow.com/questions/2481269/how-to-make-a-simple-c-makefile)
