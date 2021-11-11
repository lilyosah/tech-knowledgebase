# JavaScript
#📥 
%%
#SWE 
#coding
#concept

**Related:**
-  [[Coding Languages and Frameworks]]
-  [[jQuery]]

%%

- Runs in browsers
- JSAPI gives it power to script browsers 
- Single-threaded, all interactions with browser must be non-blocking

![[Document Object Model (DOM)]]

Separation of concerns: Do not embed JS directly in HTML, link to another script 
`<noscript>` tags happen when the browser does not support JS


## Syntax
C-like - curly braces and semicolons. Not required, but insertion is done on compilation and this process is not fool-proof, so you should include them. 
`"use strict";` at the top of the file enables stricter JS interpreter processing.
JSLint also helps to detect bad JS

## Basics 
Data types: `String`, `Array`, `RegExp`, `Object` (Hash)
`null`: explicitly empty val
`undefined`: assigned to vars that have not been initialized

### Scoping
==`let`==: block scope. Local to whatever block they're declared in
==`var`==: function or global scope. 
- If used in a func, is available anywhere in the function, **even if it hasn't been declared yet,** because they are "hoisted" to the top of the function

==global:== using neither `let` nor `var` declares global
- Become attributes of the global object (`window` in a browser)

### Regular Expressions
[[Regular Expressions]]
Can use `new RegExp("whatever")` or `/whatever/`

**Ex: ✏**  
```Js
"13346-9999".match(/^\d{5}-\d{4}/);
// or
let regex = new RegExp("^\\d{5}-\\d{4}")
"13346-9999".match(regex)

```

### Arrays
Weird things:
- No OOB errors, will just be undefined
- You can use keys and values in arrays
	- Length will not include these elements, but if you iterate through you will see them
- If you add an element at an index far off of the end, the length will include the number of undefined elements in-between the end and the new inserted element 

**Ex: ✏**  Arrays
```JS
let arr1 = [1, 2, 3];
arr1.push(4);
arr1.push(new Date());
```

### Objects (Hashes)
There are no classes - only objects. Every object has a prototype that it inherits from. When some lookup fails in that objects, consults the parent prototype, so it inherits functions and values. 

```JS
let student = {name: 'JS', classes: [class1, class2]}
```

Can access using brackets or `.`

**Ex: ✏**  Count words
```JS
function CountWords(str) {
	let hash = {};
	let words = str.toLowerCase().split(/\S+/);
	for (let i = 0; i < words.length; i++) {
		if (hash[words[i]] === undefined) {
			hash[words[i]] = 0;
		}
		hash[words[i]]++;
	}
	return hash;
}
```

#### Prototype inheritance
❗ **Must use `this` keyword to make new object.** If you don't, `this` refers to the global object. To avoid this, include `"use strict";` at the top 

**Ex: ✏**  Square "class"
```JS
"use strict";
// "class" square is capitalized by conventoin
function Square(side_length) {
	this.side = side_length;
	this.area = function() {
		return this.side_length * this.side_length
	};
}

// "instance"
var someSquare = new Square

// --- OR, better ---

function Square(side_length) {
	this.side = side_length
}

Square.prototype.area = function() {
	return this.side_length * this.side_length}
}


```

**Ex: ✏**  Dessert
```JS
"use strict";

function Dessert(name, calories) {
	this.name = name;
	this.calories = calories;
}

Dessert.prototype.isDelicious() {
	return !/licorice/i.test(this.name);
}

Dessert.prototype.isHealthy() {
	return this.calories < 200;
}


var d = new Dessert("pudding", 600);
d.isHealthy // => False
```


### Other weird shit
#### Two types of equality

`==`: implicit type conversions
-  `5 == '5'` => `true`

`===`: no implicit conversions
- `5 === '5'` => `false`

#### Idiomatic type conversion
`"13"` to string: `+"13"`

#### Functions
- First class objects and closures, you can pass references to functions

Two ways to create: function statements or function expressions

```JS
// Declared
function sum(a, b) {}

// Function expressions, can be passed
var sum = function(a, b) {}
```

## Module pattern
Define functions that execute in-place
Used to avoid adding more than you need to to the global namespace, only the module gets added and not all of its vars
- Creates variable scope
- Executed in-place

```JS
var mymodule(function() {
	var count; // this variable is "private"
	
	return {
		init: function() {
			count = 0;
		},
		click: function() {
			count++;
		},
		getCount: function() {
			return count
		}
	}
	
}());

mymodule.init();
for (var i = 0; i < 3; i++) { mymodule.click(); }

```
