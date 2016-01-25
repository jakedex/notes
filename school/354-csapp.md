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
* Threads multiple execution units
* Virtual memory is an abstraction that provides each process with the illusion that it has exclusive use of the main memory
    * each process has same *virtual address space*, or uniform view of memory
* Layers of addresses (starting at lowest):
    * *Program code and data*: Code begins at the same fixed address for all processes, followed by data locations that correspond to global C variables
    * *Heap*: Runtime heap, expands and contracts dynamically at run time as a result of calls to C std library routines
    * *Shared Libraries*: middel of address space is the area that holds the code and data for shared libraries like the C standard library and the math library. 
    * *Stack*: at the top of the user's virutal address space is the user stack that the compiler uses to implement function calls. Expands and contracts dynamically during the execution of the program with function calls and returns
    * *Kernel virtual memory*: Very top region of the address space is reserved for the kernel 
* A file is just a sequence of bytes - every I/O device is modeled as a file

### Important Themes
* *Amdahl's Law*: The observcation that when we speed up one parts of a system, the effect on the overall system performance depends on both how signifcant this part was and how much it sped up
* *Concurrency* refers to the general concept of a system with multiple, simultaneous activies
* *Paralellism* refers to the use of concurrency to make a system run faster
* *Thread-Level Concurrency*: we can have multiple control flows executing w/in a single process
    * Multiprocessors, specifically multi-core processors, each CPU core has its own L1 and L2 cache and register, with a shared L3 cache and main memory between all cores
    * * Hyperthreading*: allows single CPU to execute multiple flows of control. It involves hhaving multiple copies of some of the CPU hardware, 
* *Instruction-Level Parallelism*
    * executing multiple instructions at one time
    * Processors that can sustain execution rates faster than 1 inst/cycle are known as superscalar processors
* *Single-Instruction, Multiple-Data Parallelism*
    * allows a single instruction to cause multiple operations to be performed in parallel


