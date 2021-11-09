# JavaScript
#📥 
%%
#SWE 
#coding
#concept

**Related:**
-  [[Coding Languages and Frameworks]]

%%

- Runs in browsers
- JSAPI gives it power to script browsers 
- Single-threaded, all interactions with browser must be non-blocking

==Document Object Model (DOM):== Hierarchical, language-independent representation of [[HTML]]
- Browser parses HTML/XML -> Creates DOM
- Some incompatibility between browsers, but [[jQuery]] can help mask the differences

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
```JS
let student = {name: 'JS', classes: [class1, class2]}
```

Can access using brackets or `.`

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
