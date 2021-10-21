# Model-View-Controller (MVC)
#📥 
%%
#topic
#concept
%%
**Related:**
-  [[Design Patterns]]
-  [[Rails Views]]
-  [[Rails Models]]

---

## Definition
- Goal: Separate organization of data (model) from UI and presentation (view) by introducing a controller
	- [[Rails Routing|URI routes]] maps action to model 
- Way to organize the server application in Client-Server Architecture
- [[Ruby Rails]] supports MVC

### Components
==Models:== Store data about one entity
- Business logic work goes here
- [[Rails Models]]


==Controllers:== Mediate user actions requesting access to data
- Mediator between view and model
- Requests come in the form of [[Networks|HTTP routes]]
- Must determine which code should be invoked to handle that route
- [[Rails Controllers]]


==Views:== Display data from models which has been manipulated by controllers on a webpage
- Code should really not go here... If you absolutely need it, you can use `app/helpers`
- [[Rails Views]]

## Where errors may happen
Request
v 
route match (400)
- if fail, 404/ 400 error
- if success, invoke controller method
Controller (500 errors, you could explicitly throw a 400 error but it doesn't really make sense)
- Model errors
- View errors

If there is like an input error with `permit` etc. this is still considered 200 bc on the [[Networks]] side of things it's okay, something you need to deal with as client