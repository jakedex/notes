# C++ I/O

### Standard input and output
* write to stdout with `cout << x << y << endl;`, code evaluated from left to right
* read in with `cin >> x;`
* use `#include <iostream>`

### File I/O
* To read from a file, use variable of type `ifstream`, to write, `ofstream`
```c
 #include <fstream>
   
 ifstream inFile;
 inFile.open("input.dat");
 if (inFile.fail()) {
    cerr << "unable to open file input.dat for reading" << endl;
    exit(1);
 }
```
* `cerr` standard error
* can use `while (inFile >> n) {...}`, or `inFile.get(c)`

### I/O Parameters
* `istream` and `ostream` can be used as params (w/o the worry of whether it's stdio or a file)
* `void f( istream & input, ostream & output )` use `&` to pass by reference 

