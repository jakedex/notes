# Python Notes
My notes on [The Python Tutorial](https://docs.python.org/3.5/tutorial/)

### 3 An Informal Introduction to Python
#### 3.1 Using Python as a Calculator
##### 3.1.1 Numbers
* division always returns a floating point number
* use `//` for floor division
* `**` for powers

##### 3.1.2 Strings

* Strings can use single or double quotes
* Raw strings allow characters prefaced by `\`` to not be interpreted as special characters
* e.g. `print(r'C:\newline\filename')`
* `'''` or `"""` for multi-line Strings 
* Strings can be repeated with `*`
* Two Strings next to e/o are automatically concatenated
	* e.g. `'Py''thon'`
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
* any non-zero integer value is true, zero is false. moreover, any sequence with non-zero length is true, empty sequences are false * statements are group by indentation: * e.g. 
```python
while b<10:
		print(b)
		a,b = b, a+b
```
* `print()` writes the value of the args it's given. (e.g. `print('The value is ', 256)`)
	* argument _end_ can be used to avoid newline after output (e.g. `print(b, end=', ')`

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

* e.g.
```python
 	words = ['cat','dog','window']
	for w in words:
        	print(w, len(w))
```

* if you need to use a traditional for loop, and iterate over a sequence 
of numbers, use the built-in function `range()`
```python
		 for i in range(5):
		print(i) 0 1 2 3 4
```
	* `range(5,10)` => 5 through 9
	* `range(0,10,3)` => 0, 3, 6, 9
	* `print(range(10))` => `range(0,10)`, we say `range()` is iterable
	* `list()` is an iterator, e.g. `list(range(3))` => [0,1,2]

#### 4.4 `break` and `continue` Statements, and `else` Clauses on loops

* `break` breaks out of the smallest enclosing `for` or `while` loop 
* Loop statements can have `else` clause, it is executed when loop condition becomes false. Not executed when loop is terminated by a `break` statement * `continue`, continues with the next iteration of the loop

#### 4.5 `pass` Statement
* does nothing, used for syntactical markup
	* e.g.
	```python
	class MyEmptyClass:
		pass
	```

#### 4.6 Defining Functions
* `def function_name(param)`
* first statement of the function body can be a string, called docstring
* used to automatically produce documentation * execution of function creates new local variable symbol table
* variable references are checked in the following order: local, local of enclosing, global, built-in
* params created in local symbol table of the function, _pass by referece_ 
* function definition creates the function name in the currrent symbol table.
	* the value of the function name has a type **user defined function**. This allows the following:
		```python
		fib # this is a function
		<function fib at 1000301de0>
		f = fib
		f(100)
		```

* functions without a `return`, return `None`

#### 4.7 More on Defining Functions
* It's possible to define functions with a variable number of arguements 
- there are three forms of doing so.
 
#### 4.7.1 Default Arguement Values
* A default value can be specified for one or more arugments, this allows a function to be called with fewer arguments than it is defined to allow
	* e.g. `def ask_ok(prompt, retries=4, complaint='Yes or no, please'):` 
	* `in` keyword tests whether a sequence contains a value
	* e.g. `a = 'yes'	if a in ('yes','no','maybe')` 
	* default value is shared between calls, in turn, if it's a mutable object, like a string, you can append onto it

#### 4.7.2 Keyword Arguments
* functions can be called using keyword arguments
	* e.g. `def fun(level)` can be called with `fun(level=5)` 
	* keyword arguments must follow positional arguments 
	* a final parameter of the form `**name`, recieves a dictionary containing all keyword arugments that don't correspond to a formal param 
	* this can be combined with a parameter `*name` when recieves a tuple containing the positional arguments beyond the formal parameter list

#### 4.7.4 Unpacking Argument Lists
* To unpack arguments out of a list or tuple for a function call, use `*list_name`
	* e.g.
	```python
		args = [3,6]
		list(range(*args)) => [3,4,5]
	```

#### 4.7.5 Lambda Expressions
* small anonymous function scan be created with the `lambda` keywork 
* they are restricted to a single expression 
* e.g.
 ```python
	>>> def make_incrementor(n):
	...  return lambda x: x + n ...
	>>> f = make_incrementor(42) f(0)
	42
	>>> f(1)
	43
```

#### 4.7.6 Documentation Strings
* first line should be a short summary of the object's purpose 
* second line should be blank

#### 4.7.7 Function Annotations
* stored in the __annotations__ attribute of the function as a dictionary 
* param annotations defined by colon after param name, e.g.  `name: str` 
* return annotations are defined by `->str`
	* e.g. `def f(ham: str = 'burnt') -> str:`

#### 4.7.8 Coding Style
* wrap lines at 79 char 
* use _PEP 8_ style guide 
* use CamelCase for classes and snake_case for functions and methods

### 5 Data Structures
* has methods: append(x), extend(x), insert(i,x), remove(x), pop([i]), clear(), index(), count(), sort(key=None, reverse=False), reverse(), and copy() 
* `insert`, `remove`, and `sort` - methods that only modify the list, return the default `None` 
* __Using Lists as Stacks__
	* to add item to top, use `append()`
	* to remove from top, use `pop()` 
	* __Using Lists as Queues__
	* could use inserts and pops at beginning of list, but that's slow as each item would need to be shifted by one
	* use `collections.deque`

#### 5.1.3 List Comprehensions
* provide a concise way to create lists.
	* e.g. `squares = [x**2 for x in range(10)]`
	* consists of brackets containing expression followed by a `for` clause, and additional `for` or `if` clauses
	* e.g. `[(x, y) for x in [1,2,3] for y in [3, 1, 4] if x!= y]`

#### 5.2 The `del` Statement
* way to remove item from list given its index instead of its value, differs from `pop()` method which returns a value
	* e.g. `a = [-1, 0, 1] del a[0]` 
	* can also be used to delete entire variables

#### 5.3 Tuples and Sequences
* along with strings and lists, tuples are also a _sequence_ data type 
* consists of a number of values separated by commas 
* tuples may be nested 
* tuples are immutable 
* on output, tuples are enclosed in parentheses 
* accesses via unpacking or indexing 
* usually heterogeneous sequence, vs list homogeneous 
* empty tuples `empty = ()` 
* single value `single = 'hello',` 
* sequence unpacking: `x, y, z = t`

#### 5.4 Sets
* unordered collection with no duplicate elements 
* `{'im creating', 'a', 'set'}` or `set('creating','a')` to create a set
	* note that `set()` must be used for empty sets - `{}` creates empty dictionary 
	* can perform set union, difference, intersection, and symmetric difference

#### 5.5 Dictionaries
* 'associative array', indexed by keys, which can be any immutable type (stings and numbers usually used) 
* keys must be unique 
* `list(d.keys())` returns list of all keys used in dictionary 
* `dict(key1=44, majorkey=9, key2=23)`

#### 5.6 Looping Techniques
* when looping through dictionaries, the key and corresponding value can be retrieved at the same time using `items()` method
	* e.g. `for k, v in dict.items():`
* the equivalent for a sequence, which would include index and corresponding value can be retreieved using the `enumerate()` method
* to loop over multiple sequences at the same time, use the `zip()` method
* `sorted()`, and `reversed()` methods also utilized

#### 5.7 More on Conditions
* conditions used in `while` and `if` can contain many different operators like the following
	* `in`, and `not in` check whether value occurs in sequence
	* `is` `is not` compare whether two objects are really the same object
	* `and`, `or` are both _short-circuit_ operators
* In Python, assignment cannot occur inside expressions

#### 5.8 Comparing Sequences and Other Types
* Sequence comparison uses lexicographical ordering:
	* first two items are compared, and so on
	* if sub-sequence of the other, shorter is the lesser one
	* strings are comparing with unicode code point number

### 6 Modules
* Python's way to put definitions into a file and use them as a script or in an interactive instance of the interpreter
* definitions from a module can be imported into other modules or into the main module, the colletion of variables that you have acces to in a script executed at the top level and in calculator mode
* w/in a module, the module's name (as a string) is available as the value of the global var `__name__`
	* e.g. `import module`, `module.__name__` => `'module'`

#### 6.1 More on Modules
* to import functions/variables directly into the importing module's symbol table, `from fibo import function_name, var_name`
	* note this doesn't import `fibo`
* when running module as script, i.e. `python mod.py <args>`, it will be executed, just as it would on import, but with `__name__` set to `__main__`
* module search path: built in -> .py in `sys.path`
* Python caches the compiled version of each module in `__pycache__` under the name `module.version.pyc`

#### 6.4 Packages
* way of structuring Python's module namespace (e.g. module name `A.B` designates submodule named `B` in package `A`
```python
sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```
* `__init__.py` files are required to make Python treat the directories 
as containing packages

### 7 Input and Output
#### 7.1 Fancier Output Formatting
* `str.format()` is Python's printf()
	* e.g. `print('{0} and {1}'.format('spam', 'eggs'))` => 'spam and eggs'
	* can also use more traditional `%` formatting
	* `print('The value of PI is approximately %5.3f.' % math.pi)`
* `str()` generates human readable representations of values
* `repr()` generates representations that can be read by the interpreter

#### 7.2 Reading and Writing Files
* `open()` returns a file object
	* `open(filename, mode)`
* `f.read()`, `f.readLine()`
* numbers => `json` called *serializing*, use json.dump(data, file)
* `json` => numbers, *deserializing*, use json.load(file) 

### 8 Errors and Exceptions
#### 8.3 Handling Exceptions

```python
try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
    except OSError as err:
        print("OS error: {0}".format(err))
    except ValueError:
        print("Could not convert data to an integer.")
    except:
        print("Unexpected error:", sys.exc_info()[0])
        raise
```
* can also have `else:` statement at end that execs if try didn't throw
* `finally` works like in java
* raising exceptions: `raise NamError('Hey there')`
* user defined exceptions: 
	```python
	    class MyError(Exception):
	        def __init__(self, value):
	            self.value = value
	        def __str__(self):
	            return repr(self.value)
	```
* `with` statement allows objects like files to be cleaned up properly
	* e.g. 
	```python
	with open("myfile.txt") as f:
	    for line in f:
	            print(line, end="")
	```

### 9 Classes
#### 9.2 Python Scopes and Namespaces
* *namespace* is a mapping from names to objects. I.e. the set of attributes of an object also form a namespace
* use `nonlocal` to define module level variables inside functions, and `global` to define global variables
	* e.g. 
	```python
	def do_nonlocal():
	    nonlocal spam
	    spam = "nonlocal spam"
	def do_global():
	    global spam
	    spam = "global spam"
	```

### 9.3 A First Look at Classes
* Class objects support two kinds of operations: attribute references and instantiation
	* attribute refereces (e.g. `obj.name`), valid names are all names in class's namepspace
		* can be assigned to
	* Class instantiation uses function notation (e.g. `x = MyClass()`)
		* Instantation operation creates an empty object
		* For constructor, use method named `__init__()`
			* e.g.
			```python
			def __init__(self, realpart, imagpart):
			    self.r = realpart
			    self.i = imagpart
			```
#### 9.3.3 Instance Objects
* Instance objects have attribute reference operations (data attributes, and methods)
* data attr or *instance variables*, methods are just functions that belong to an object

#### 9.3.4 Method Objects 
* `x.f` is a method object, whereas `MyClass.f` is a function object
* usually method is called like `x.f()`, but it can be stored `xf = x.f` for later use `xf()`
* Methods pass the object as the first argument of the function, i.e. `x.f() == MyClass.f(x)`
* In general, calling a method with a list of the n arguments of an object is equvalent to calling the corresponding function with an argument list that is created by inserting the method' object before the first argument

#### 9.3.5 Class and Instance Variables
* class and instance variables behave in the same way as Java
* data atr override method atr
* often, first argument of a method is called `self`

#### 9.5 Inheritance
* `class DerivedClassName(BaseClassName)`
* Derived classes may override methods of their base classes
* To extend a base class method, `BaseClassName.methodname(self, arguments)`
* `isinstance(obj, int)` checks class inheritance, `issubclass(bool, int)`

#### 9.5.1 Multiple Inheritance
* `class DerivedClassName(Base1, Base2, Base3)`

#### 9.6 Private Variables
* Private instance variables don't exist in Python
* However, convention is `__spam` should be treated as non-public
* _Name mangling_ changes any identifier of the form `__spam` to `_classname__spam`, the avoids the issue with subclasses with the identical method names as their base class but without overriding ocurring. 
* Empty class can act like Pascal's 'record' data type
	* e.g. 
	```python
	class Employee:
	    pass

	    john = Employee() # Create an empty employee record

	    # Fill the fields of the record
	    john.name = 'John Doe'
	    john.dept = 'computer lab'
	    john.salary = 1000
	 ```

#### 9.9 Iterators
* when `for ele in [1,2,3]: `, behind the scences the `for` statement calls `iter()` on the object

#### 9.10 Generators
* written like regular functions but use `yield` statement to return data
* 

### 10,11 The Standard Library
* _in progress..._


### 12 Virtual Environments and Packages
* virtual environment is a self-contained directory tree that contains a Python installation for a particular version of Python plus a number of addtional packages

#### 12.2 Creating Virtual Environments
* `pyvenv <directory>` installs python virtual environment
* then run, `source <directory>/bin/activate`
* with a virtual env, you can manage packages with pip
* use `pip freeze > requirements.txt` and `pip install -r requirements.txt`

