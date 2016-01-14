# Python Notes

###  The Python Book
#### Get started with Python
* List: contains a collection of data in a specific order
* Tuple: Contains a collection of immutable data in a specific order
* Dictionary: Stores data in key-value pairs
* Variables are dynamically typed
* 

### Python Docs
#### 3 An Informal Introduction to Python
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

#### `if` Statements

