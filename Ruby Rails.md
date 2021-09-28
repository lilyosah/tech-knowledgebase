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

## Philosophy
- **Convention over Configuration**
	- If naming follow certain conventions, no need for config files
- **Don't Repeat Yourself (DRY)**
- **Sharp Knives are Provided**
	- Introspection and metaprogramming
	- Blocks (closures)
	- Modules (Mix-ins)

## Structure / Design Pattern
- Uses [[Design Patterns#Model-View-Controller MVC]]
	- Each Rails model is a resource type whose instances are rows in a particular table of a relational database 
	- Rails routing subsystem maps HTTP routes to code in the app that performs the correct action
- Convention over configuration
- Uses [[Relational Databases]]
	- What is the relationship between how an instance of a resource is stored in the database and how it's represented in a particular programming language used by the framework?
	- What mechanisms mediate those representations?
	- For rails: [[Design Patterns#Active Record]]


## Making an App
- A class that descends from `ActiveRecord::Base` provides methods needed to connect model to the database
- `$ exec rails g(enerate) model`
	- Default table is model name in all lowercase with an s added at the end
		- Model `Book` -> BD table `books`
		- `TimeSheet` -> `time_sheet`
	- Lets you do everything except create the table, to do that you must create a ==migration:== a [[Ruby]] script describing a set of changes to make to the database schema
		- Do this instead of using SQL because Rails defines production environments, you'd have to make three identical SQL calls 
		- `$ exec rails g(enerate) migration [migration name]`
		- To add to the table, have to add to the seed

### In-class
- New creates git repo, gem file
- Can

```Bash
$ gem install rails
$ rails new

Can help initally to --skip-tests --skip-javascript --skip-bundle
```

- In gem files, dependencies and their versions are lsited
- Separate groups for each env
	- Ex: in `:development, :test`, may include rspec

```Bash
$ bundle config --without production
Installs gems in every env aside from production

$ rails server launches the sesrver
launches in localhost:3000
```

- Server usually live-updates, if you change routes or server configurations you must relaunch the server 

#### Routes 
Map incoming URLs to controller actions and extract optional parameters 
- Wildcare paramters:


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