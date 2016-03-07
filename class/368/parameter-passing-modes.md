# Parameter Passing Modes 
## Overview
* `void f( int a, int &b, const int &c );` a is passed by value, b reference, and c const-reference

## Value Parameters
* when passed by value, a copy of the parameter is made and no changes made to the formal parameter by the called function have any effect on the actual parameter
* note that if a pointer is passed by value, the object pointed to by the pointer can be changed e.g.
```c
void f(int *p) {
    *p = 5;
    p = NULL;
}

int main() {
    int x=2;
    int *q = &x;
    
    f(q);

    // here, x == 5, but q != NULL
}
```

## Reference Parameters
* When a parameter is passed by referece, conceptually, the acutal parameter itself is passed (just given the name of the corresponding formal parameter). changes made to the formal parameter _do_ affect the actual parameter. 
* swap functions are easy this way -
```c
void swap( int &j, int &k ) {
    int tmp = j;
    j = k;
    j = tmp;
}
```

## Const-Reference Parameters
* can declare parameter `const` to make sure it isn't changed when using references parameters out of wanting to avoid copying a large param
* member functions that do not modify any data members should be declared const as the compiler will complain that they are changing const-reference parameters otherwise

## Array Parameters
* Arrays are always passed by reference
* Use a vector if you want to pass an array by value
