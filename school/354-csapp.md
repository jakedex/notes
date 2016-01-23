# CS 354 - Computer Systems: A Programmer's Perspective Notes
## Chapter 1
* Source file: created in an editor and saved with `.c`
    * Byte/character
    * Text file - consist of only ASCII characters
* C was developed from 1963-1973 by Dennis Richie of Bell Labs. 
    * ANSI ratified the ANSI C standard in 1989, standards were later taken over by ISO. These include the C standard library. 
    * Unix written almost entirely in C

### C compilation system
hello.c (Source program) => [Pre-processor (cpp)] => hello.i (Modified source program) => [Compiler (cci)] => hello.s (Assembly program) => [Assembler (as)] => hello.o + prinf.o (Relocatable object programs (binary)) => [Linker (ld)] => hello (Executable object program (binary))

* *Preprocessing phase*: The preprocessor (cpp) modifies the original C program according to directives that begin with the '#' character. E.g. `# include <stdio.h>`
* *Compilation phase*: The compiler (cc1) translates the text file into an assembly language program
* *Assembly phase*: Assembler (as) translates assembly language file into machine language instructures, in a form known as a relocatable object program (binary)
* *Linking phase*: Linker (ld) handles merging of our program with functions that were called from the standard library. The result is an executable file. 

#### Side Note: The GNU project
* Short for GNU's Not Unix
* charity started by Richard Stallman in 1984
* Goal of developing UNIX-like system w/o source code restrictions

* Buses carry bytes of information to the various components. Transfer fixed-size chunks of bytes called words (word size of 8 bytes => 64 bits)
* I/O devices are connected to the I/O bus by controllers/adapters
* Main memory,consisting of DRAM chips, holds the program and data it manipulates while the processor is executing it
* Use Caches to serve as temporary staging areas
    * L1 cache: tens of thousands of bypes, access is nearly as fast as the register file
    * L2 cache: larger, connected to processor by special bus, ~5x slower than L1
    * Implmented with SRAM
* L0 (register) > L1 > L2 > L3 > Local disks > Network disks
    * Storage at one level serves as a cache for the one below it
* Process: os's abstraction for a running program
* With unicore systems, CPU can only execute one program at a time - but can appear to execute multiple processes concurrently by having the processor switch amoung them (context switching)
    * The os keeps track of the state (context) information the process needs to run
    * System calls pass control of the OS
    * Transitions from one process to another are managed by the kernel
* Threads
