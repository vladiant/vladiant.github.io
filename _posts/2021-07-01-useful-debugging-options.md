---
layout: post
title: "Useful Debugging Options"
date: 2021-07-01
tags: c++ debug
---

## readelf
* [readelf](https://man7.org/linux/man-pages/man1/readelf.1.html)

### readelf -S
* -S | --section-headers | --sections
* Displays the information contained in the file's section headers, if it has any.

### readelf -x tool.c.o
* -x number_or_name | --hex-dump=number_or_name
* Displays the contents of the indicated section as a hexadecimal bytes.  A number identifies a particular section by index in the section table; any other string identifies all sections with that name in the object file.

### readelf -R mytool
* -R number_or_name | --relocated-dump=number_or_name
* Displays the contents of the indicated section as a hexadecimal bytes.  A number identifies a particular section by index in the section table; any other string identifies all sections with that name in the object file.  The contents of the section will be relocated before they are displayed.

### readelf -Ds
* -D | --use-dynamic
* When displaying symbols, this option makes readelf use the symbol hash tables in the file's dynamic section, rather than the symbol table sections.
* When displaying relocations, this option makes readelf display the dynamic relocations rather than the static relocations.

## objdump
* [objdump](https://linux.die.net/man/1/objdump)

### objdump -h tool.c.o
* -h | --section-headers | --headers
* Display summary information from the section headers of the object file.
* File segments may be relocated to nonstandard addresses, for example by using the -Ttext, -Tdata, or -Tbss options to ld. However, some object file formats, such as a.out, do not store the starting address of the file segments. In those situations, although ld relocates the sections correctly, using objdump -h to list the file section headers cannot show the correct addresses. Instead, it shows the usual addresses, which are implicit for the target.

### objdump -s -j.text tool.c.o
* -s | --full-contents
* Display the full contents of any sections requested. By default all non-empty sections are displayed.
* -j section | --section=section
* Display information only for section name.

### objdump -Mintel -d -j.text tool.c.o
* -M options | --disassembler-options=options
* Pass target specific information to the disassembler. Only supported on some targets. If it is necessary to specify more than one disassembler option then multiple -M options can be used or can be placed together into a comma separated list.
* -d | --disassemble
* Display the assembler mnemonics for the machine instructions from objfile. This option only disassembles those sections which are expected to contain instructions.

### objdump -Mintel -r -j.text tool.c.o
* -r | --reloc
* Print the relocation entries of the file. If used with -d or -D, the relocations are printed interspersed with the disassembly.

### objdump -drS useful.c.o
* -S | --source
* Display source code intermixed with disassembly, if possible. Implies -d.

### objdump -t CMakeFiles/mytool.dir/tool.c.o
* -t | --syms
* Print the symbol table entries of the file. This is similar to the information provided by the nm program, although the display format is different.

### objdump -T mytool
* -T | --dynamic-syms
* Print the dynamic symbol table entries of the file. This is only meaningful for dynamic objects, such as certain types of shared libraries. This is similar to the information provided by the nm program when given the -D (--dynamic) option.

## hexdump
* [hexdump](https://man7.org/linux/man-pages/man1/hexdump.1.html)

### hexdump -C CMakeFiles/mytool.dir/tool.c.o
* -C | --canonical
* Canonical hex+ASCII display.  Display the input offset in hexadecimal, followed by sixteen space-separated, two-column, hexadecimal bytes, followed by the same sixteen bytes in %_p format enclosed in '|' characters.  Invoking the program as hd implies this option.

## ldd
* [ldd](https://man7.org/linux/man-pages/man1/ldd.1.html)
* Print shared object dependencies

## gdb
* [gdb](https://man7.org/linux/man-pages/man1/gdb.1.html)

### list [file:]function
* type the text of the program in the vicinity of where it is presently stopped.

### disas STARTADDRESS ENDADDRESS
* Displays a range of memory as machine instructions.

### stepi
* Execute one machine instruction (follows a call).

### print *(void**)0x
* Display the value of an expression.

### where
* Where the program is, i.e. where the segmentation fault occurred

### info reg
* List contents of registers.

## Reference
* [What Does the Linker Actually Do for Us? - CB Bailey & Andy Balaam](https://www.youtube.com/watch?v=M2jn2ttRex0)

## Reference source tool.c
```c
#include <stdio.h>

int perturb(int a)
{
   return a - 1;
}

int main(void) {
   printf("%d\n", perturb(0));
   return 0;
}
```
