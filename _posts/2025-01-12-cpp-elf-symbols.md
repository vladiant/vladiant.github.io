---
layout: post
title: "C++ ELF symbols"
date: 2025-01-12
tags: c++ design development debug
---

## Sections
* text section -  instructions and read-only data
* data section - initialized writable data
* bss section - uninitialized data

## Related commands
`objdump -s values.o`
* Display the full contents of sections, often used in combination with -j to request specific sections.

`objdump -j name values.o`
* Display information for section name.

`objdump -d values.o`
* Display the assembler mnemonics for the machine instructions from the input file.

`objdump -t values.o`
* Print the symbol table entries of the file. This is similar to the information provided by the nm program, although the display format is different.

`nm values.o`
* lists the symbols from object files

`readelf -SW values.o`
* Displays the information contained in the file's section headers, if it has any.
* Don't break output lines to fit into 80 columns.

## Relocations
* `objdump -dr -M intel values.o`
* Display the assembler mnemonics for the machine instructions from the input file.
* Print the relocation entries of the file.
* Pass target specific information to the disassembler.

## Final binary
* `objdump -d -M intel the_program`

## If there were no symbols
* `gcc -o the_program values.o main.o`
* `nm values.o`
* `strip values.o`
* `nm values.o`
* `gcc -o the_program values.o main.o`

## Linkage
* `nm values.o`

## C++ headers
* `nm -C values.o`
* Decode (demangle) low-level symbol names into user-level names. 

## Weak symbols
* `nm values.o main.o`

## Linking weak symbols
* `objdump -h main.o | grep .text`
* Display summary information from the section headers of the object file.

## Controlling visibility
* `target_compile_options(dynlib PRIVATE -fvisibility=hidden)`
* `readelf -s values.o`
* Displays the entries in symbol table section of the file, if it has one.

## References
* [How Linux Elf Symbols Work and How They Are Used in C++ and C Programming - Anders Schau Knatten](https://www.youtube.com/watch?v=X2jFjeCDOYw)
* [GCC sections](https://gcc.gnu.org/onlinedocs/gcc-5.3.0/gccint/Sections.html)
* [objdump](https://man7.org/linux/man-pages/man1/objdump.1.html)
* [nm](https://linux.die.net/man/1/nm)
* [readelf](https://man7.org/linux/man-pages/man1/readelf.1.html)
* [strip](https://www.man7.org/linux/man-pages/man1/strip.1.html)
* [target_compile_options](https://cmake.org/cmake/help/latest/command/target_compile_options.html)
* [GCC Visibility](https://gcc.gnu.org/wiki/Visibility)