# Ruby Rails
#📥 
%%
#coding 
#concept
%%
**Related:**
-  [[Ruby]]
-  [[SaaS (Software as a Service)]]
-  [[Relational Databases]]

---

- Uses [[Design Patterns#Model-View-Controller MVC]]
	- Each Rails model is a resource type whose instances are rows in a particular table of a relational database 
	- Rails routing subsystem maps HTTP routes to code in the app that performs the correct action
- Convention over configuration
- Uses [[Relational Databases]]
	- What is the relationship between how an instance of a resource is stored in the database and how it's represented in a particular programming language used by the framework?
	- What mechanisms mediate those representations?
	- For rails: [[Design Patterns#Active Record]]
	- A class that descends from `ActiveRecord::Base` provides methods needed to connect model to the database
		- Lets you do everything except create the table, to do that you must create a ==migration:== a [[Ruby]] scrip
