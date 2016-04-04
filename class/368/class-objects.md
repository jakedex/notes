# Differences in creating class objects.

a) pointer
```
Example* example=new Example();
```
// you get a pointer, and when you finish it use, you have to delete it:
```
delete example;
```

b) Simple declaration
```
Example example;
```
you get a variable, not a pointer, and it will be destroyed out of scope it was declared.
