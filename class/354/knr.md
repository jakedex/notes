# Notes on The C Programming Language (K&R)
## Chapter 1
* Program begins executing at `main` function
* variables usually declared all at beginning
* `printf` works like in Java
* comments same as Java
* symbolic constants: `#define` line defines a symbolic name or symbolic constant to be a particulat string of characters, `#define name replacement text`
* *text stream* is a sequence of characters divided into lines, each line with zero or more characters followed by a newline character
* `getchar()` reads next input character from a text stream, `putchar(c)` prints a character 
* can use `int` to store `char` 
* any assignment is an expression and has a value (value of the left hand side after the assignment)
    * `while((c = getchar()) != EOF)`
    * above parentheses are required, `!=` has higher precedence than `=`
* *null statement*, an isolated semicolon, satisfies C's requirement of for a `for` loop to have a body
* `int power(int base, int n)`
* *function prototype* is a function declaration before main
* All arguments are passed 'by value' - called function is given the values of its arguments in temp variables rather than the originals
* `\0` is the null character, whose value is 0, is placed at the end of a char array to mark the end of a string of characters
* local variables are often referred to as automatic variables, as they disappear automatically when the function is exited
* global variables often called external variables
    * must be defined outside any function
    * variable must also be declared in e function that wants to access it - explicitly with `extern int max;`
    * `extern` not need when definition of the external variable occurs in the source file before its use in a particular function
    * Traditionally, all `extern` declarations of variables and functions are placed in a separate file called a header, that is included by `#include` at the front of e/ source file (suffix .h)
    * `void` should be included in function prototypes with empty param list
* 'Definition' refers to places where the variable is created or assigned storage, 'declaration' refers to places where the nature of the variable is state but no storage is allocated

## Chapter 2
* With the ANSI standard, there are now signed and unsigned forms of integers
* variables are case sensitive, alphanumeric

### Data Types and Sizes
* `char` a single byte
* `int` typically the natural size of integers on the host machine
* `float` single-precision floating point
* `double` double-precision floating point
* can apply `short int sh;` and `long int counter`, yet same as when int is omitted
* `long double`

### Constants
* a long constant: `123456789L`, unsigned long constant: `1236789UL`
* integer specified in octal: leading `0`, integer specified in hex: `0x`
* Strings concatenated `"hello, " "world"`
* enumeration: `enum boolean { NO, YES };`
    * first name in enum has value 0, second 1, and so on (unless explicit values are specified)

### Declarations
* `int lower, upper, step;`
* `const` can be applied to the declaration of any variable to specify that it's value will not be changed
* can also be used with array arguments, to indicate that the function does not change the array
     * `int strlen( const char[]);`

### Type Conversions
* implicit for lossless conversions
* casting works the same as in Java

### Bitwise Operators
* & AND, | OR, ^ XOR, << left shift, >> right shift, ~ one's compliment (unary)
* can be used on integral operands - int, char, short, int, and long

### Assigment Operators
* +=, -=, *=, /=, %=, <<=, >>=, &=, ^=, |=

### Conditional Expressions
* ternary operator: expr1 ? expr2 : expr3
*

## Chapter 3: Control Flow 
* braces group declarations and statements together into a block
* else statement is associated with the closest 'else-less' if
* else-if structure same as JAva
```c
switch (expression) {
    case const-expre: statements
    case const-expre: statements
    default: statements
}
```
* do while is same as Java
* break, continue same as Java
* `goto` can be used to break out of multiple loops
```c 
for (...)
    for (...) { 
        if (disaster)
            goto error;
    }

error: 
    ...
```

## Chapter 4: Functions and Program Structure
* if return type is omitted, int is assumed
* calling routine must know that a function returns a non-int value
    * explitily: `double sum, atof(char []);`
    * if there's no function prototype, a function is implicitly declared by its first apprearance in an expression, which is then assumed to return an int - and nothing is assumed about its arguments

### External Variables
* Defined outside of any function
* Functions themselves are external, as C doesn't allow nested functions
* By default, all references to external objects by the same name are references to the same thing (external linkage)

### Scope Rules
* Scope of an external object lasts from the point at which it is declared to the end of the file being compiled
* if external variable is to be referred to before it is define, or it is defined in a different source file from the one where it is being used, then an `extern` declaration is manditory
* declaration simply announces the properties of a variable, and a definition actually sets storage aside
    * `int sp;` declares and defines the external variable sp, whereas `extern int sp;` simply declares the variable sp but does not set aside any storage, etc
    * must only be one definition of an external variable amoung all the files that make up a program
    * array sizes must be specified w/ the definiton, but are optional w/ an `extern` declaration

### Header Files
* Place definitions and declarations shared amoung project's files into one central file and have the others `# include` it

### Static Variables
* `static` declaration, applied to external object, limits the scope of that object to the rest of the source file being compiled
* normally functions are global, visible to any part of the entire program - can be declared static so that its name is invisible outside of the file in which it is declared
* Internal variables can also be static, which makes them remain in existance rather than coming and going each time the function is activated

### Register Variables
* `register` declaration advises the compiler that the variable in question will be heavily used - and are placed in machine registers
* can only be applied to automatic variables and formal parameters of a function

### Block Structure
* Variables that follow the left brace that introduces any compound statement hide any identically named variables in outer blocks and remain in existance until the matching right brace
* Automatic variables, including formal parameters, hide external variables and functions of the same name

### Initialization
* In the absense of explicit initialization, external and static variables are guaranteed to be initialized to zero, automatic and register variables have underfined (garbage) values
* Arrays can be initialized with same shorthand as Java

### The C Preprocessor
* File inclusion - `#include "filename"` or `#include <filename>`, source lines are replaced by the contents of the file *filename* upon precompilation
    * an included file in quotes starts searching where the source program is found
* Macro Substitution - `#define name replacement_text`, occurrences of the token *name* will be replaced by the *replacement_text*
    * possible to define macros with arguments
    * unset with `#undef name`
* Conditional inclusion - `#if !defined(HDR)`


## Chapter 5: Pointers and Arrays
* A pointer is a variable that contains the address of a variable
* operator (&) gives the address of an object, `p = &c;` assigs the address of c to the var p
* `*` is the indirection or dereferencing operator - accesses the object the pointer points to 
* unary operators: operate on a single operand, e.g. `++`, `--`, `!`, `*`
    * associate right to left, so `(*ip)++` requires parenth

### Pointers and Function Arguments
* to implement swap function, pass pointers as arguments `swap(&a, &b)`

### Pointers and Arrays
* if `int *pa = arr;`, then `pa` points to `arr[0]`, and `*(pa + 1)` increments `pa` to the next element in the array
* since the name of an array is a synonym for the location fo the initial element,`pa = &a[0]` is the same as `pa = a` and `a[i]` == `*(a+i)`
* you can also use `pa[i]` with pointers
* when an array name is passed to a function, it's simply the address of the initial element being passed in - so, instead of `char s[]` as a parameter, we can and should use `char *s` as it's more explicit

### Address Arithmetic
* Can use pointers to allocate/free blocks of memory
* C guarantees that 0 is never a valid address for data
* `NULL` is definied in `<stdio.h>`
* pointers can be compared, is `p` and `q` point to members of the same array, then relations like `==`, `<`, etc work properly
* pointer subtraction is also valid; if `p` and `q` are as defined above, and `p<q`, then `q-p+1` is the number of elements form `p` to `q` inclusive
* `p + n` means the address of the n-th object beyond the one `p` is currently pointing to - regardless of what kind of object `p` points to (scaled)

### Character Pointers and Functions
* `char amessage[] = "now is the time";` is an array, and `char *pmessage = "now is the time";` is a pointer
    * in the array, inidivual characters can be changed but it will always refer to the same storage
    * in the pointer, it's initialized to point to a string constant, the pointer can be modified to point elsewhere, but you can't change the contents

### Pointer Arrays; Pointers to Pointers
* can have `char *lineptr[10000];`

### Multidimensional Arrays
* Can had 2D array, just an array of arrays
* To pass to 2D array to function, parameter def must include the number of columns, e.g. `f(int daytab[][13]) {..}`

### Pointers vs. Multi-dimensional Arrays
* `int a[10][20];` sets aside 200 int-sized locations
* `int *b[10];` assuming each element of `b` does point to a int[20], then 200 int-sized locations are set aside, along with 10 pointer locations, with the advantage that the rows of the array can be different lengths

### Command line arguments
* main is called with two arguments, the first being `argc` and second `argv`, the number of arguments and a pointer to an array of character strings
* by convention, `argv[0]` is the name by which the program was invoked, so `argc` is always at least 1
* `argv[argc] = '\0'`

### Pointers to Functions
* `int (*comp)(void *, void *)` : `comp` is a pointer to a function that has two `void *` args and returns an int

### Complicated Declarations
* `int *f()` - a function returning pointer to int, while `int (*pf)()` a pointer to a function returning int
* `char (*(*x())[])()` : x is a function returning a pointer to array[] of pointer to function returning char

## Chapter 6: Structures
* A structure is a collection of one or more variables, grouped together under a single name for conveinient handling
```c 
struct point {
    int x;
    int y;
};
```
* variables named in a structure are called members
* `struct` declaration defines a type - so `struct { ... } x, y, z;` is analogous to `int x, y, z;`
* can include tag to reference strcuture and for use in definitions of instances of the structure
    * `struct point { int x; int y; };`
* to initialize: `struct point maxpt = { 320, 200 };`
* refer to members with structurename.member
* can be nested
    * `struct rect screen` -> `screen.pt1.x`

### Structures and Functions
```c
stuct point makepoint(int x, int y)
{
    struct point temp;

    temp.x = x;
    temp.y = y;
    return temp;
}
```
* generally advised to pass pointers instead of large structures as arguments, to access member - `(*sp).x`, as `*sp.x` isn't a pointer in this case
* alternative notation `sp->x`
* structure operators are at the top of the precedence hierarchy: `.`, `->`, `()`, and `[]`

### Arrays of Structures
```c
struct key {
    char *word;
    int count;
} keytab [NKEYS];
```
* instead of making two parallel arrays, just make an array of structs

### Self-referential Structures
* illegal for a structure to contain an instance of itself, but can have pointers to an instance of itself
```c 
struct tnode {
    char *word;
    int count;
    struct tnode *left;
    struct tnode *right;
}
```

### Typedef
* `typedef` is a facility for creeating new dat type names
    * `typedef int Length` makes the name `Length` a synonym for `int`
* Used to parameterize a program against portability issues, and to provide better documentation

### Unions
* A union is an object that may hold objects of different types and size, with the compiler keeping track of size and alignment requirements
* syntax based on structures
```c 
union u_tag {
    int ival;
    float fval;
    char *sval;
} u;
```
    * `u` will be large enought to hold the largest of the three types
    * any of the types may be assigned to `u`, as long as the usage is consistant
* members accessed same way as structures
* can only be initialized with the type of its first member

### Bit Fields
* A *bit-field* is a set of adjacent bits w/in a single implementation-defined storage unit that we will call a 'word'
* define a variable called `flags` that contains three 1-nbit fields:
```c
struct {
    unsigned int is_keyword : 1;
    unsigned int is_extern : 1;
    unsigned int is_static : 1;
} flags;
```
* number following the colon represents the field width in bits
* may only be declared as ints

## Chapter 7: Input and Output
* I/O is not a part of the C language itself, but are contained in the standard library

### Standard input and output
* simplest input mechanism is to read one character at a time from the standard input with `int getchar(void)`
    * returns next input char each time it's called, or `EOF` when it encounters theend of file
* `<` can be used to substitute file for input redirection: `prog <infile`
* `int putchar(int)` puts the char c on the std output and returns EOF if an error occurs
* `>` output can be redirected to a file name
* i/o library functions are included in `stdio.h`

### Formatted Output - Printf
* `printf` translates internal values to characters
* returns the number of characters printed
* (http://www.tutorialspoint.com/c_standard_library/c_function_printf.htm)[http://www.tutorialspoint.com/c_standard_library/c_function_printf.htm]

### Variable-length Argument Lists
* `<stdarg.h>` contains a set of macro definitions that define how to step through an argument list

### Formatted Input with Scanf
* `scanf` is input analog of `printf` : `int scanf(char *fmt, ...)`
* each argument following *fmt must be a pointer to the location of where to store the var
* to read input lines that contain dates of the form 25 Dec 1988, 
```c
int day, year;
char monthname[20];

scanf("%d %s %d", &day, monthname, &year);
```
* scanf ignores the blanks and tabs in its format string and skips over whitespace as it looks for input values

### File Access
* `FILE *fopen(name, mode)` returns a file pointer - a structure that contains info about the file
* `FILE` defined with `typedef`
* modes include 'r', 'w', and 'a'
* to read, write FILEs - use `int getc(FILE *fp)` and `int putc(int c, FILE *fp)`
* upon starting a C program, the operating system environment opens the following three files and provides file pointers to them - stdin, stdout, and stderr
* `getchar` and `putchar` can be defined like `#define getchar()    getc(stdin)`
* `fclose(FILE *fp)` breaks the connection between the file pointer and the external name that was established with `fopen`, and flushes the buffer 
    * `fclose` is called automatically for each open file when a program terminates normally

### Error Handling - Stderr and Exit
* `stderr` output stream appears normally on the screen, even if the stnd output is redirected
* w/in main , return expr is equivalent to exit(expr)
* `int ferror(FILE *fp)` returns non-zero if an error occurred on the stream fp

### Line input and Output
* `char *fgets(char *line, int maxline, FILE *fp)` reads the next input line (including newline) from file fp into the character array line; at most maxline-1 characters will be read
* `int fputs(char *line, FILE *fp)` writes a string to a file

### Storage Management
* `void *malloc(size_t n)` returns a pointer to n bytes of uninitialized storage
* `void *calloc(size_t n, size_t size)` returns a pointer to enough space for an array of n objects of the specified size, or NULL if the request cannot be satisfied 
* The storage is initalized to zero
* POINTER MUST BE CAST INTO THE APPROPRIATE TYPE
    * int *ip;
    * `ip = (int *) calloc(n, sizeof(int));`
* `free(p)` fress the space pointed to by `p`, where `p` was originally obtained by a call to `malloc` or `calloc`
* Don't free anything that isn't obtained from `m|calloc`

## Chapter 8: The UNIX System Interface
* UNIX provides its services through set of system calls - which are in effec tfunctions within the os that may be called by user programs

### File Descriptors
* In the process of opening a file, the system checks your right to do so - if all goes well, the system returns to the program a small non-negative integer called a *file descriptor*
    * whenever I/O is done on the file, the file descriptor is used instead of the name to identify the file (analogous to a file pointer in C)
* since I/O with the keyboard and screen is so common, when the shell runs a program, three files are open, with file descriptors 0, 1, and 2, called the standard input.... , resp. 
* User can redirect I/O with `<` and `>`, e.g. `prog <infile >outfile`

### Low Level I/O - Read and Write
* read,write system calls are accessed from C programs through functions `read` and `write`
    * `int n_read read(int fd, char *buf, int n);`

### Open, Creat, Close, Unlink
* the `open` system call returns a file descriptor (int)
    * `int open(char *name, int flags, int perms)`
* `int creat(char *name, int perms)` system call creates new files, or re-writes old ones

### Random Access - Lseek 
* system call `lseek` provides way to move around in a file without reading or writing any data
    * `long lseek(int fd, long offset, int origin)`
    * origin can be 0, 1, or 2 to specify that offset is to be measured from the beginning, the current position, or from the end of the file respectively

### Example - Listing Directories
* Directory is simply a file with a list of filenames and inodes (where all info besides filename is kept)

### Example - A Storage Allocator
* Free storage is kept as a list of free blocks of storage with each block containing a size, a pointer to the next, and the space itself (control info at beginning is called a header)
* When a request is made, the free list is traversed until a big enough block is found (first fit), once found, the block is unlinked from the list and returned to the user
* If the block is too big, it's split and the correct size is unlinked and returned to the user
* If the there are no blocks large enough, more space is requested from the OS and added to the list
* All blocks are multiples of the correctly aligned header
