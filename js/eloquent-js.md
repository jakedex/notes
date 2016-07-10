# Eloquent Javascript Notes

* only functions define new scopes

* *Declared Function*: `function asdf() {}` is set up right away, can be used before defined

* obj.name gives name prop

* obj[name] evaluates name and gives prop of result

* push/pop add and remove from end, shift/unshift add and remove from front

* can't add properties to strings, num and Boolean as they are immutable

* arguments var is created on func call

* having too many vars pollutes the global namespace, JavaScript doesn't warn you when creating obj or car that's already w the name

* global scope obj is window

* *higher order functions*: functions that operate on other functions, take them as arguments, or return functions

* json: all property names surrounded by double quotes, no func calls or anything that involves actual computation, no comments

* `JSON.stringify` / `JSON.parse`

* filter method on arrays is pure, doesn't alter content, returns new arr

* `bind()` creates a new function that calls the original with some values of arguments already fixed

* `this` points to object being called upon

* all objects have a prototyped that's used as a fallback source of properties, when gets request for prop it doesn't have, prototype will be searched

* Some don't directly have obj proto, Function.prototype, Array.prototype

* constructors are functions called w new keyword

* convention to captalize names of functions

* all functions have prop prototype which contains empty obj that derives from obj.prototype

* Adding new method: `Rabit.prototype.speak = function`

* properties we create by assigning values to them are enumerable, whereas those in proto are nonenumerable

* use function `Object.defineProperty()` to add enum props

* `Object.create(null)` creates wo proto

* getter:
```
get height() {
    return this.elements.length;
}
```

* `.call()` method calls a function with a given this value and arguments provided individually.

* `.apply()` method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

* `.bind()` method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

* `RTextCell.prototype = Object.create(TextCell.prototype);`

* strict mode- throws error on undef vars instead of creating global. this binding holds value undefined in functions not called as methods. when outside of strict, this refers to the global scope object

* `debugger` keyword is the equivalent to setting a breakpoint and opening the debugger

* *first-class functions*: supports passing functions as args to other functions, returning them as values to other functions and assigning them to variables, etc

* `new RegExp('abc')`

  * /abc/.test()

* only two scopes, local function and global.

* `var dayName = function()` unnamed function

* can wrap in function and ()() to force it be interpreted as an expression

* commonjs modules w node js

* AMD uses define function and takes an array of module names and a function as args, calls function after running all modules

* domain specific language - a language tailored to express a narrow domain of knowledge

* TCP: transmission control protocol, one computer is listening of other computers to start talking to it. to be able to listen to different kinds of communication at the same time on a single machine, each listener has a port associated with it.

* CSS: cascading style sheets

  * The precedence rule only holds true  when the rules have the same specificity

  * positioning:
	   * static: default,
	   * relative: enables top, left
	   * absolute: top, left used to absolutely position it relative to the top-left corner of the nearest enclosing element whose position property isn't static

* propagation goes from the node to its parent to the root of the document
	* stopPropogation()
	* preventDefault()

* No two scripts can run at the same time

* Web workers allow for an isolated JS environment that runs alongside the main program for a document and can communicate with it only by sending and receiving messages

  `new Worker('code/worker.js')`

* xmlns changes element to a different XML namespace

* promises pass an asynchronous action around in an object
  * promisejs.com

* remote procedure calls - function runs on another machine, call w function name, args, and receive result

* `process` variable, is global in node provides various ways to inspect and manipulate the current program.

* document and alert are absent from node

* window -> global in node

* objects that emit events have method `on` that is similar to addEventListener in the browser

  * readable streams have 'data' and 'end' events, the first called every time something comes in

* content type indicators like text/plain are also called MIME types

* function inlining simply brings in the code from the method call into the function making that call so that control doesn't have to change.

* each function call gets its own this binding, so even in the constructor for Grid, we can't write to this.grid - instead the other function creates a normal local variable, grid, through which the inner function gets access to the grid.
	* common workaround is to say var self = this and then refer to self in the inner functions.
	* or use .bind(this)

* `Array.prototype.map()` creates a new array with results of a provided function on every element in this array
