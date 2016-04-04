# Classes with Pointer Data Members - Notes
Every class that has a pointer data member should include the following member functions:
    * a destructor,
    * a copy constructor,
    * operator= (assignment)

## Destructor Functions
An objects destructor function is called when that object is about to 'go away', i.e.
    * when class object (value parameter or local variable) goes out of scope
    * when a pointer to a class object is deleted

Memory leaks occur without a destructor

## Copy Constructor Functions
An object's copy constructor is called (automatically, not by the programmer) when it is created, and needs to be initialized to be a copy of an existing object. This happens when an object is:
    * passed as a value parameter to a function,
    * returned (by value) as a function result,
    * declared with initialization from an existing object of the same class.

The purpose of the copy constructor is to make a copy of the
    * actual parameter,
    * value being returned,
    * existing object.

If you don't write a copy constructor, the compiler will provide one that just copies the value of each data member (this is sometimes called a shallow copy). If some data member is a pointer, this causes aliasing (both the original pointer and the copy point to the same location), and may lead to trouble.

### The Copy Constructor Declaration
e.g.
```
class IntList {
  public:
      IntList();                 // default constructor
          IntList(const IntList &L)  // copy constructor
            ...
            };
```

### The Copy Constructor Definition
The copy constructor should copy the values of all non-pointer data members, and should copy the objects pointed to by all pointer data members (this is sometimes called a deep copy).

## Operator=
If a class includes pointer fields, the default class assignment causes aliasing, and as we have seen in the case of the copy constructor, this can lead to trouble! For example, if the L2.Items array is full when the assignment is done, then a subsequent call to L1.AddToFront will cause the array to be returned to free storage (so L2.Items will become a dangling pointer).

The default assignment can also cause storage leaks when the class has a pointer field. For example, when L1 = L2; is executed, L1.Items is simply overwritten with the value in L2.Items, the array that L1 was pointing to is not returned to free storage (and that storage is now lost).

To prevent these problems, you should always define operator= as a class member function for a class with a pointer field, and you should define operator= to do a deep copy. The declaration of the member function looks like this for the IntList class:
```
IntList & operator=(const IntList &L);
```
The idea is that when the assignment L1 = L2; is executed, L1's member function operator= is called, and L2 is passed as the argument to that function.

Note that IntList's operator= function returns an IntList. This is to permit chained assignment, for example: L1 = L2 = L3;

Note that operator= differs from the copy constructor in three important ways:
    * The object being assigned to has already been initialized; therefore, if it has a pointer field, the storage pointed to must be freed to prevent a storage leak.
    * It is possible for a programmer to assign from a variable into itself; for example: L1 = L1. The operator= code must check for this case, and do nothing.
    * The operator= code must return a value.
