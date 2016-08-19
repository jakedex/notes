# [Let's Learn ES6 Notes](https://www.youtube.com/playlist?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX)

## let, const, and Template Literals

### let

Allows for block scoping of variables. 

```
if(true){
	let name = "Jake";
}

console.log(name); // Reference error, not defined
```

### const

Adds `final`/read-only functionality to JS

### Template Literals

Allows for multiline Strings, better concatination with String interpolation

```
let name = `Jake
This is a new line`
```

```
console.log(`My name is ${name}`);
```

### Shortened Method Signatures

```
let person = {
	firstName: 'Jake',
	sayName() {
		return `HI I'm ${this.firstName}`
	}
}
```

## Arrow Functions

```
let add = (a,b) => {
	return a + b;
}
```

or even shorter (taking advantage of implicit return and the fact that's it's a single line function), 

```
let add = (a,b) => a + b;
```

you can even do things like, 

```
[2, 3, 4, 6, 7].map( n => n * 2);
```

Also allow for lexical scoping, so no more `var self = this;` (!!!), breaks arguements keyword, though. 

## Spread Operator and Rest Parameters

### Rest Parameters

```
let sum = function(...args) {
	return args.reduce(prev, curr) => prev + curr;
});
```

## Spread Operator

Removes need for cases like the following:

```
let numbers = [3, 5, 5, 6];
let max = Math.max.apply(null, numbers);
```

By providing something like an inverse use of rest parameters:

```
let numbers = [3,4,5,6];
let max = Math.max(...numbers);
```

Another use case,

```
let numbers = [5,3,3,5];
let newNumber = [3,5,6,2,...numbers,4,5];
```

## Destructoring 

A new way to access/pick and choose properties on objects and arrays

```
let person = { age: 30 };
person.age; // 20
person['age']; // 20
let { age: personAge } = person;
// property: variable to store in = from object

let { age } = person;
console.log(age);
```

```
let key = "age";

let { [key] : keyAge }  = person;
// finds 'age' property on object
```

With arrays:

```
let nums = [2,3,4,6];

let [first, second,, fourth] = numbers;
console.log(fourth);
```

Common use case with React:

```
import { Router, Route, Link } from 'react-router';

```

## Promises

```
let myPromise = new Promise((success, fail) => {
	setTimeout(() => {
		success('yay');
	}, 500);
	
	fail('oh no');
});

myPromise.then((res) => {
	console.log(res);
}, (err) => {
	console.log(err);
});

// or 

myPromise.then((res) => {
	console.log(res);
})
.catch((err) => {
	console.log(err);
});
```

### ES6 promises:

```
let myPromise2 = new Promise((resolve, reject) => {
	setTimeout(() => {
		resolve('Promise 2 - the promising');
	}, 1500);
});

// returns new promise once given are done
Promise.all([myPromise, myPromise2])
	.then((data) => {
		console.log(data);
	});
```

### fetch

```
fetch('http://google.com')
	.then((res) => {
		console.log(res.json().then((data) => {
			console.log(data);
		}));
	})
	.catch((err) => {
		console.log(err);
	});
```

## Modules

Default exports:

```
// -- mod.js
// each file can have only one default export
export default function(text) {
	console.log(`Modules are ${text}.`);
}

// -- app.js
import testMod from './mod';

testMod('neat!');
```

Named exports: 

```
// -- math.js
export function add(a, b) {
	return a + b;
}

export const substract = (a,b) => {
	return a - b;
}

export default function() {
	return a / b;
}

// -- app.js
import { add, subtract } from './math';

add(2,3); // 5
subtract(4, 2); // 2
```

Also can import with:

```
import * as myMath from './math';
myMath.add(3,2); // 5
myMath(10,2); // default export - 10
```

To bring in default when there are named: 

```
import divide, {add, subtract} from './math';
```
