# Operator Overloading - Notes
C++ allows almost all operators to be overloaded to apply to class objects.

Note also that when you overload operators, at least one operand must be a class object (or an enum).

## Example: Overloading +=
In the statement:
```
L1 += 10;
```
the left operand of += is an IntList, and its right operand is an integer. Therefore, this version of += can be defined either as an IntList member function or as a free function. Here is how it might be defined as a member function:
```
class IntList {
  public:
    void operator+=( int n );
  ...
};

void IntList::operator+=( int n ) {
  AddToEnd( n );
}
```

## Example: Overloading <<
In the statement:
```
cout << L1;
```
the left operand of `<<` is an ostream, not an IntList. Therefore, operator `<<` cannot be defined as a member function of the Intlist class; it must be defined as a free function. For example:
```
ostream &operator<<( ostream &out, const IntList &L ) {
  L.Print(out);
  return out;
}
```

Function declared as `friend` can access private data members

