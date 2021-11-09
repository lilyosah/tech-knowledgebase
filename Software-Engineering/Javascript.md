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

Document Object Model (DOM): Hierarchical, language-independent representation of [[HTML]]
- Browser parses HTML/XML -> Creates DOM
- Some incompatibility between browsers, but [[jQuery]] can help mask the differences

Separation of concerns: Do not embed JS directly in HTML, link to another script 
`<noscript>` tags happen when the browser does not support JS


## Syntax
C-like, curly braces and semicolons. Not required, but insertion is done on compilation and this process is not fool-proof, so you should include them. 
`"use strict";` at the top of the file enables stricter JS interpreter processing.
JSLint also helps to detect bad JS
