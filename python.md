# Python Notes

###  The Python Book
#### Get started with Python
* List: contains a collection of data in a specific order
* Tuple: Contains a collection of immutable data in a specific order
* Dictionary: Stores data in key-value pairs
* Variables are dynamically typed
* 

### Python Docs
### 3 An Informal Introduction to Python
#### 3.1 Using Python as a Calculator
##### 3.1.1 Numbers
* division always returns a floating point number
* use `//` for floor division
* `**` for powers

##### 3.1.2 Strings

* Strings can use single or double quotes
* Raw strings allow characters prefaced by `\` to not be interpreted as 
special characters
	* e.g. `print(r'C:\newline\filename')
* `'''` or `"""` for multi-line Strings 
* Strings can be repeated with `*`
* Two Strings next to e/o are automatically concatenated
	* e.g. `'Py''thon'` *
* Strings can be indexed with `word[0]`
	* Index can be negative, to start counting from the right
* No separate character type - character is simply a string of size one
* Slicing (substrings) e.g. `word[0:2] => 'Py'`
	* start included, end excluded
	* out of range slice don't throw errors
* Strings are immutable
* `len()` returns length of string
* are sequence type
#### 3.1.3 Lists

* can contain items of different types
* lists are the most versatile compound data type
* can be indexed and sliced (e.g. `items[-1:99]`)
	* slice copy: `words[:]`
* concatenation (e.g. `items + [1, 2, 3]`)
* lists are mutable
* `append()` to add new items at the end of the list
* lists can be nested

### 3.2 First Steps Towards Programming

* multiple assignment: `a,b = 0,1`
* any non-zero integer value is true, zero is false. moreover, any 
sequence with non-zero length is true, empty sequences are false
* statements are group by indentation:
* e.g. ```python
while b<10:
		print(b)
		a,b = b, a+b
```
* `print()` writes the value of the args it's given. (e.g. `print('The 
value is ', 256)
	* argument _end_ can be used to avoid newline after output (e.g. 
`print(b, end=', ')

### 4 More Control Flow Tools

#### 4.1 `if` Statements
```python
if x < 0:
	x = 0
	print('negative to zero')
elif x == 0:
	print('zero')
elif x == 1:
	print('one')
else:
	print('more')
```

#### 4.2 `for` Statements

* e.g. ```python
words = ['cat','dog','window']
for w in words:
	print(w, len(w))
```

* if you need to use a traditional for loop, and iterate over a sequence 
of numbers, use the built-in function `range()`
	* ```python
for i in   range(5):
	print(i)
0
1
2
3
4
```
	* `range(5,10)` => 5 through 9
	* `range(0,10,3)' => 0, 3, 6, 9
	* `print(range(10))` => `range(0,10)`, we say `range()` is 
iterable
	* `list()` is an iterator, e.g. `list(range(3))` => [0,1,2]

#### 4.4 `break` and `continue` Statements, and `else` Clauses on loops

* `break` breaks out of the smallest enclosing `for` or `while` loop
* Loop statements can have `else` clause, it is executed when loop 
condition becomes false. Not executed when loop is terminated by a 
`break` statement
* `continue`, continues with the next iteration of the loop

#### 4.5 `pass` Statement
* does nothing, used for syntactical markup
	* e.g. ```python
	class MyEmptyClass:
		pass
	```

#### 4.6 Defining Functions
* `def function_name(param)
* first statement of the function body can be a string, called docstring
	* used to automatically produce documentation
* execution of function creates new local variable symbol table
	* variable references are checked in the following order: local, 
local of enclosing, global, built-in
	* params created in local symbol table of the function, _pass by 
referece_
* function definition creates the function  name in the currrent symbol 
table. 
	* the value of the function name has a type _user defined 
function_. This allows the following: 
		```python
		fib # this is a function
		<function fib at 1000301de0>
		f = fib
		f(100)
		```

* functions without a `return`, return `None`

#### 4.7 More on Defining Functions
* It's possible to define functions with a variable number of 
arguements - there are three forms of doing so.
 
#### 4.7.1 Default Arguement Values
* A default value can be specified for one or more arugments, this 
allows a function to be called with fewer arguments than it is defined 
to allow
	* e.g. `def ask_ok(prompt, retries=4, complaint='Yes or no, 
please'):`
* `in` keyword tests whether a sequence contains a value
	* e.g. `a = 'yes'	if a in ('yes','no','maybe')`
* default value is shared between calls, in turn, if it's a mutable 
object, like a string, you can append onto it

#### 4.7.2 Keyword Arguments
* functions can be called using keyword arguments
	* e.g. `def fun(level)` can be called with 'fun(level=5)`
* keyword arguments must follow positional arguments
* a final parameter of the form `**name`, recieves a dictionary 
containing all keyword arugments that don't correspond to a formal param
* this can be combined with a parameter `*name` when recieves a tuple 
containing the positional arguments beyond the formal parameter list

#### 4.7.4 Unpacking Argument Lists
* To unpack arguments out of a list or tuple for a function call, use 
`*list_name` 
	* e.g. ```python
	args = [3,6]
	list(range(*args)) => [3,4,5]
	```

#### 4.7.5 Lambda Expressions
* small anonymous function scan be created with the `lambda` keywork
* they are restricted to a single expression
* e.g. ```python
>>> def make_incrementor(n):
...     return lambda x: x + n
...
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43
```

#### 4.7.6 Documentation Strings
* first line should be a short summary of the object's purpose
* second line should be blank

#### 4.7.7 Function Annotations
* stored in the __annotations__ attribute of the function as a 
dictionary
* param annotations defined by colon after param name, e.g. `name: str`
* return annotations are defined by `->str`
	* e.g. `def f(ham: str = 'burnt') -> str:`

#### 4.7.8 Coding Style
* wrap lines at 79 char
* use _PEP 8_ style guide
* use CamelCase for classes and snake_case for functions and methods

### 5 Data Structures

