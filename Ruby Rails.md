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
	- `$ exec rails g(enerate) model`
		- Default table is model name with an s added
		- Lets you do everything except create the table, to do that you must create a ==migration:== a [[Ruby]] script describing a set of changes to make to the database schema
			- Do this instead of using SQL because Rails defines production environments, you'd have to make three identical SQL calls 
			- `$ exec rails g(enerate) migration [migration name]`
			- To add to the table, have to add to the seed

## [[SQL]] Calls in Rails
[[Networks#Representational State Transfer REST|CRUDI]]
- **SELECT** `[Model].all`
- **SELECT WHERE** `[Model].where("year >= 2000")`
	- Can be chained, like
		- `[Model].where("year >= 2000").where("year <= 2020")`
- **Create/INSERT** `Model.create(attribute: "The Perks of being a Wallflower", year: 1999)
	- If you don't specify attributes, default to `nil`/`null` (for databases)
- **Update/Read** `Model.find(9)` Takes ID
	- So save in the table, save the found object with `item.save!`
- **Delete** `item.destroy`