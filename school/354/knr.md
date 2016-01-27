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
* 
