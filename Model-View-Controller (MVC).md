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
	- URI routes maps action to model 
- Way to organize the server application in Client-Server Architecture
==Models:== Store data about one entity 
==Controllers:== Mediate user actions requesting access to data
[[Rails Views]]
- Requests come in the form of HTTP routes
- Must determine which code should be invoked to handle that route
- [[Ruby Rails]] supports MVC