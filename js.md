# Javascript - Understanding the Weird Parts
## Section 2
Lexical Environment: Where you write something is important.
Execution context: Wrapper to help manage and group code that is running.
Object is simply a collection of name-value pairs

Base execution context is global
  Creates Global Object, and 'this'

In browser, window is the global object
At global level, this refers to window
global = not inside a function

When creating global variables and fuctions, they get attached to the global object

Execution context
  Creation phase: Global object, 'this', outer env
    Hoisting: Memory space for variables and functions is set up
      functions are placed in entirety into memory
      variables only initialized to undefined
        undefined is a special value that means it hasn't been set
  Execution phase: runs code line by line

Javascript is single threaded, sychronous by default

