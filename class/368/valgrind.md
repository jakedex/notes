# Valgrind Notes
* Some of the things that valgrind can detect are:
    * bad array indexes
    * bad pointer dereferences (e.g., deferencing an uninitialized pointer, dereferencing a NULL pointer, or dereferencing a dangling pointer)
    * storage leaks

## How to use
Compile your program as normal.  It is the executable that is will be checked by valgrind.
```
g++ -g main.cpp
valgrind a.out
```
(As usual, use the -o flag to produce an executable named something other than a.out.)


