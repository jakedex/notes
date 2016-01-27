# Introduction

## Basic Terminology and C++ functions
* Java has fields and methods, C++ data members and functions
* *free functions* are functions that aren't inside any class
* Every C++ program must include free function called main 
    * should return type int - error codes, so `0` to indicate normal termination, and any non-zero value to indicate the an error occurred
    * to run program w/ command line arguments, `int main( int numargs, char *args[] )`
    * print to stdout: `std::cout << "Hello, world!" << std::endl;`
        * `<<` output operator can be used to write a value of any of the primitive types
* Assignment operator is *right associative*, so `x = y = z = 0` is evaluated right-to-left 
* Whereas the output operator is left associative, so `std::cout << x << y << y;` x is printed first, then y, etc
* `# include <iostream>` is similar to import in java - note it doesn't have a semi-colon
* to declare `std::cout` with just `cout`, use a namespace declaration - `using namespace std;`
* define functions/variables before using them, compiles top to bottom
* *forward declaration* allows use of functions/variables before implementation
     ```c
        # include <iostream>
        using namespace std;

        void print();

        int main() {
            print();
                return 0;
                }

         void print() {
            cout << "Hello world!" << endl;
         }```
* `g++ -o foo foo.cpp`

## C++ Types
### Primitive (built-in) types
* essentially same as Java: int, char, bool, float, and double
* integers can be used as booleans, can use `if (0 == x)` to avoid this issue
* `const int MAXSIZE = 100;`

### Arrays
* No length operation, no runtime check for out of bounds index, no arraycopy function, can't change size dynamically
* Often better to use `vector` class - which is an autoexpanding array
* `int A[10]` declares array and allocates required memory

### Enumerations
* New types with a fixed (usually small) set of possible values: `enum Color { red, blue, yellow }`, define with `Color col = blue;`

### Structures
* Used to group logically related values together, similar to a C++ class
```c
struct Student {
    int id; 
    bool isGrad;
};
```
* Note that the decl must end with a `;`

### Unions
* Similar to struct declaration, but fields all share the same space - only one 'active' field

### Pointers
* a point variable contains either an address or special value `NULL` (must include `stdlib.h` to use)
    * Can contain: address of some variable, address of some dynamically allocated memory, or the address of a function
    * e.g. `int *p;`
    * `&` address of operator, e.g. `int *p = &x;`
    * assign p to the address in a chunck of storage allocated dynamically with the `new` operator
        * `int *p = new int;`
    * to access the location pointed to by a pointer p, use the `*` operator
        * `cout << *p;`
    * `==` compares the addresses stored in the pointers, not the values (use `*p == *q`)
* Unlike Java, there's no garbage collection - this means if you allocate memory from the heap, that memory can't be reused unless you deallocate it explicitly (using `delete` operator)
* In general, for every `new` use, need to have a corresponding `delete` statement
* commonly used to point to a structure, e.g. if p points to structure with a field named f, it can be accessed with `(*p).f` or its shorthand `p->f`
* also commonly used to point to dynamically allocated array of values: `int *p = new int [10];`
    * to return the array to free storage, use `delete[] p`
    * can then access each array element by incrementing the pointer, e.g. `*p = 5` same as `p[0] = 5`, and `p++` for `p[1]`
* `typedef` to define a new type with the same range of values/operations as an existing type
    * e.g. `typedef double Dollars;`
