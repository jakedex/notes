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

## Chapter 2: REpresenting nad Manipulating Information
* Leogardo Pisano (Fibonacci) brought the decimal system to the west from India
* floating point arithmatic is not associateive due to the finite precision of the representation
* The international Standards Organization took over standardization of the C language in 1990, thus ISO90, and released an updated ISO99 in 1999. `gcc -std=c99`

### 2.1 Information Storage
* most computers use blocks of eight bits, or bytes, as the smallest addressable unit of memory

#### Hexadecimal
* When a value x is a power of two, x = 2^n, we can represent it as n = i + 4j. e.g. x=2048=2^11=n=11=3+4*2 => ox800
* decimal -> hex requires dividing the num by 16, and using the remainder as the least significant digit 
* hex -> dec is just multiply each hex digit by the appropriate power of 16

#### Words
* each computer has a word size, and because the virtual address is encoded by such word, the word size determines the maximum virtual address space

#### Addressing and Byte Ordering
* multi-byte objects are stored as contiguous seq of bytes
* least significant byte first - little endian
* msb first - big endian
* many recent microprocessors are bi-endian
* usually not a huge deal, except when networking between two machines of different types

#### Representing Strings
* strings are array of chars terminated with null char. characters are usually encoded with the ASCII character code
* Unicode standard has over 100,000 characters for encoding text in many languages
    * UTF-8 encodes each character as a sequence of byte, such that all ASCII characters use the same single byte encodings as they have in ASCII
    * Java uses Unicode to represent its strings

#### Boolean Algegra
* bit vectors are strings of zeros and ones of some fixed length w
    * can be used to represent sets, and further perform set operation with boolean algebra

#### Logical Operations in C
* Logical operators short circuit, whereas bit-wise do not

#### Shift Operations in C
* the right shift operation has two forms, logical (fills from msb with zeros) and arithmetic (fills from msb with msb). C standards don't define which type of right shift should be used. generally almost everything uses arithmetic right shits for signed data

### 2.2 Integer Representations
#### Integral Data Types
* integral data types are those that represent finite ranges of integers
* unsigned range is [0,2^w)
* signed is [-2^w-1, 2^w-1)
    * twos complement's range is asymptotic, |Tmin| = Tmax + 1
* Umax = 2Tmax + 1
* there's also one's complement and sign-magnitude for representing signed numbers
* C allows casting between different numeric data types, e.g. x is an `int`, `(unsigned) x`, this simply keeps the bit values identical but changes how they are interpreted

### 2.3 Integer Arithmatic
* with a 4-bit word size, the sum could require 5 bits

### 2.4 Floating Point
* encodes raitonal numbers of the form, V=x*@^y
* IEEE floating point is the widely adopted standard: V = (-1)^s * M * 2^E
* significand M is a fractional binary number
* Cases
    * 1: Normalized values: occurs when bit pattern of exp is neither all zeros nor all ones. in this case, the exponent field is interpreted as representing a signed integer in biased form (E = e - Bias)
    * 2: denormalized: when exponent fields is all zeros
    * 3: when exponent field is all ones: when fraction field is all zeros, infinity, when nonzero, NaN


## Chapter 3: Machine-Level Representation of Programs
* GCC compiler generates output in the form of human readable assembly code, and the assembler and linker make generate the machine code from that
* Extension of IA32 to 64 bits was called x86-64, and was developed by AMD
* 64bit machines can use up to 256 TB of memory

### 3.1: A Historical Perspective
* Intel's processor line is known as x86
* Linux uses flat addressing, where the entire memory space is viewed by the programmer as a large array of bytes
* gcc flag `-01` and `-02` applies level-one and level-two optimizations, respectively

#### 3.2.1 Machine-Level Code
* the ISA, or instruction set architecture, defines the processor state, and the format of the instructions
    * e.g. IA32, x86-64
* the ISAs describe the behavior of a program as if each instruction is executed in sequence, but the actual processor hardware executes many instructions concurrently
* memory addresses used by a machine-level program are virtual addresses
* the PC, aka program counter, indicates the address in memory of the next instruction to be executed
* the integer register file contains eight named locations storing 32-bit values
    * these registers can hold addresses or integer data
* conidtion code registers hold status information about the most recently executed arithmetic or logical instruction - used to implement conditional changes in the control or data flow like if and while statements
* a set of floating point registers store floating point data
* disassemblers are used to inspect the contents of machine-code files. They generaete essentially assembly code from the machine code. use unix program `objdump`, e.g. `objdump -d code.o`
* ATT assembly code format is the default for GCC, OBJDUMP and many other unix tools. Intel format is used by Microsfot

### 3.3 Data Formats
* 16-bit data type referred to as word, 32-bit as double word
* most assembly code instructions have single-character suffix denoting the size of the operand
    * movement instr has movb (byte), movew (word), and movl(move double word)

### 3.4 Accessing Information
* register names start with `%e`

#### 3.4.1 Operand Specifiers
* specify the source and destination values of an operation
* immediate is for constant values, written with `$` followed by an integer. e.g. `$-577`
* register, denotes the contents of one of the eight registers (IA32), e.g. `%eax` for double word operation
* memory, some memory location according to an effective address (computed address)
    * many different addressing modes for memory references, most general is `Imm(Ea, Ei, s)`
        * Imm being the immediate offset Imm, a base reigster Eb, and index register Ei, and a scale factor (1|2|4|8). The effective address is then computed as Imm+R[Eb]+R[Ei]*s. 

#### 3.4.2 Data Movement Instructions
* MOV class copy source values to destinations
* source can be immediate, register, or memory
* destination can be register or memory
* move instruction cannot have both operands refer to memory locations, this requires two instructions with a register acting as an intermediate
* MOV S, D
* push and pop add/remove items to the programs stack
* `%esp` stack pointer holds the address of the top stack element
* by convention, stack is drawn with top (lowest addresses) on the bottom
* pointers are simply addresses - dereferencing a pointer involves copying that point into a register and then using this register in a memory reference
* local variables are often kept in registers over memory locations as it is much faster

### 3.5 Arithmetic and Logical Operations
* Most operations are given as instruction classes, as they have different operand sizes: byte, word, and double-word
* operations are divided into four groups: load effective address, unary, binary, and shifts

#### 3.5.1 Load Effective Address
* `leal` is just a variant of the movl instr, but instead copies the effective address to a destination register
* used to generate pointers

### 3.6 Control

#### 3.6.1 Condition Codes
* CPU maintains set of single-bit condition code registers describing attributes of the most recent arithmetic or logical operation. These can then be tested to perform conditional branches
    * e.g. CF (carry flag), ZF, SF, OF. 
    

