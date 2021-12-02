# jQuery
#📥 
%%
#SWE 
#coding 
#concept

**Related:**
-  [[Javascript]]
-  [[HTML]]
-  [[CSS]]
-  [[AJAX]]

%%

A framework for [[Document Object Model (DOM)]] manipulation
- Adds many features over browsers' built-in API

## Selecting elements
May be called 4 ways:
1. Parameter is a function
	- Waits until everything has loaded to call the function
2. Parameter is CSS selector
	- `jQuery('#main')`
	- May return several node elements but it is not an array, must use iterator
3. Parameter may be a plain DOM object
4. Parameter may be a string

## Manipulating selected elements
Can change styling, hide/show things, etc.
`e.show()`, `e.fadeOut('slow')`, `e.css('background: green')`
`e.text`, `e:ischecked`?

### Event handlers
- Links and buttons that are clickable without JS run handler first, if handler returns false, no other action is taken. Otherwise, other actions follow handler
- If you CAN do something with [[CSS]], you should

**Ex: ✏**  Click handler
```JS
jQuery('#myButton').on("click", function () {
	console.log("I love to be clicked.");
});.
```

## Dealing with Ajax
### To execute after several calls
`when`

```JS
function getData1 (){ 
 return $.get('/page1.php');
}

function getData2 (){ 
 return $.get('/page2.php');
}

function getData3 (){ 
 return $.get('/page3.php');
}

$.when(getData1(),getData2(),getData3()).done(function(r1,r2,r3){
 console.log(r1) //[data, status, xhrObj]
 console.log(r2) //[data, status, xhrObj]
 console.log(r3) //[data, status, xhrObj]
})
```