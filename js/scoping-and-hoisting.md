# [Scoping and Hoisting](http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html) Notes

## Scoping in Javascript

Unlike C-family languages, which have block-level scope, Javascript has function-level scope. This means that blocks, such as if statements, do not create a new scope. _Only_ functions create a new scope.

If you must create temporary scopes within a function, use the following pattern:

```javascript
function foo() {
	var x = 1;
	if (x) {
		(function () {
			var x = 2;
			// some other code
		}());
	}
	// x is still 1.
}
```

## Declarations, Names, and Hoisting

Names enter a scope in one of the four basic ways:

1. Language-defined: all scopes are given `this` and `arguments`
2. Formal parameters
3. Function declarations: These are of the form `function foo() {}`
4. Variable declarations: These take the form `var foo;`

Function declarations and variable declarations are always moved ('hoisted') invisibly to the top of their containing scope by the JavaScropt interpreter. This means that code like this:

```javascript
function foo() {
	bar();
	var x = 1;
}
```

is actually interpreted like this:

```javascript
function foo() {
	var x;
	bar();
	x = 1;
}
```

Notice that the assignment portion of the declarations weren't hoisted, only the name. This isn't the case for function declarations, where the entire function body is hoisted as well. The names of function expressions are hoisted, but the body is left behind.

(Recall function definitions are `function bar()`, while function expressions are `var foo = function () {}`)

## Name Resolution Order

The above four ways names enter scopes are the order they are resolved in. If a name has already been definied, it is never overridden by another property of the same name. As such, a function declaration takes priority over a variable declaration.

Weird exceptions:
  * The build-in name `arguments` behaves in a way such that it's declared before function declarations but after formal parameters. So, a formal parameter with the name `arguments` will take precendence over the built-in.
  * Trying to use `this` as an identifier anywhere will cause a Syntax error.
  * If multiple formal parameters have the same name, the one occurring latest in the list will take precedence.

## Named Function Expressions

`var baz = function spam() {}` // named function expression (only baz gets hoisted)
