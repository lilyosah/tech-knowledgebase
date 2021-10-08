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
- [[Rails Models]]
==Controllers:== Mediate user actions requesting access to data
- Requests come in the form of [[Networks|HTTP routes]]
- Must determine which code should be invoked to handle that route
- [[Rails Controllers]]
==Views:== Display data from models which has been manipulated by controllers on a webpage
- [[Rails Views]]