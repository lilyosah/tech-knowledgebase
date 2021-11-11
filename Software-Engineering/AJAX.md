# Title
#📥 
%%
#topic
#concept

**Related:**
-  

%%

Asynchronous JavaScript and XML

Using [[Javascript]] to retrieve data from a server without requiring a full page reload

- JS makes request to server 
- Server responds with data encoded in some form 

Can make requests using [[jQuery]]:

```JS
var req = jQuery.ajax({
	url: '...',
	method: 'POST',
	data: {...},
}).done(function(msg) {
	// Code that gets executed when request is done
});

```

