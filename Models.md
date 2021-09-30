# Models
#📥 
%%
#topic
#concept
%%
**Related:**
-  

---

Handles business logic in [[Design Patterns#Model-View-Controller MVC]] architecture

- 1 [[Relational Databases|Relational Database]] table = 1 model class
	- **Naming:** snake-case and plural
	- **Ex:** `books` table, `time_cards`
- 1 row = 1 model instance
	- **Naming:** Upper-camel-case and singular
	- **Ex:** `Book` class, `TimeCard`
	- Found in 	`app/models/book.rb`
- Each row has a unique primary key, automatically assigned by Rails
	- By convention, and integer called `id`

- `[Model].new` creates new model instance?

==Schema:== Collection of their tables and their structure 

 [[Design Patterns#Active Record]] 
 
 ## The Database
 - Don't destroy real user data!
	 - Rails solution: Each env has its own database, and different DB types that are appropriate for each 
	 - Development, test, production
 - Keeping env DBs consistent:
	 - ==Migrations:==

## Migrations
: a script describing changes to the database #📌 *This is mentioned somewhere else*
 - Automatable 
 - Creates the tables

Show help: `rails g model`

### Option 1
1. Create table `rails generate migration CreateBooks`
2. Apply migrations `rails db:migrate`

### Option 2
- `rails generate model`
- Creates a migration script along with `app/models/model.rb`
	- Can specify column names/types to generator, and the migration generator

### Migration Code
Can get table objects to add attributes to 
 
 
## Data Types
- `int`, `string`, `text`, `'decimal {digits, digits}'` (need single quotes around bc curly braces are special in shell), `blob` (raw binary)
- Can't have array 
 
 **Ex: ✏ Model for a product and user**  
 Model for a product:
 - `int` ID
 - `int` Quantity
 - `string` Image URL
 - `string` Name
 - `decimal` Price
 - `text` Description
 - `string` Manufacturer, maybe in another model
 - `string` Category/tags - probably in another model
 - Reviews - probably in another model

Model for a user:
- `int` ID
- `string` Username
- `string` Password
- `string` Name
- `string` Address - could be another model association or break it out here
- Payment info - in another model
- Cart IDs - another model
- Order history

## Methods
Rails generally shields us from needing to make actual SQL calls
- This is great because if different databases are used for each env you don't need to change your code
- These are provided when descending from [[Design Patterns#Active Record]] 

📝 Can do `[Model].nethods` to see massive list of methods


> ⭐ The getters and setters do not modify instance variables, it's data in the table.
> **So the class is empty, there are no actual instance variables.**
> This is why you must save after making changes to the data, otherwise the data is only in memory


### CRUDI Methods
[[Networks#Representational State Transfer REST|CRUDI]]
📝`.to_sql` method on any CRUDI method shows the corresponding SQL call at the end of any active record call

- **SELECT** `[Model].all`
	- Like `SELECT * FROM books`
- **SELECT WHERE** `[Model].where("year >= 2000")`
	- Can be chained, like
		- `[Model].where("year >= 2000").where("year <= 2020")`
		- `[Model].where("list_price < ?", 2)` interpolates `2` into `?`
		- `[Model].where("list_price < ?", "%#{match_str}%")` interpolates `match_str` into `?`
		- ❗ Do not use regular string interpolation, opens app up to SQL injection 
- **Create/INSERT** `Model.create(attribute: "The Perks of being a Wallflower", year: 1999)
	- If you don't specify attributes, default to `nil`/`null` (for databases)
- **Update/Read** `Model.find(9)` Takes ID
	- To save the data in the table after making changes, save the found object with `[Model instance].save!`
	- `[Model].find_by(key: "value")`
- **Delete** `item.destroy`
- **Create and Save** `item.create` (adding `!` throws exception)

Computations
Do not do computations in Ruby if possible, should be done in the DB
- `[Model].average('col')`
- `[Model].max('col')`
- `[Model].min('col')`

### Model Attributes
To change column data, `self.title.capitalize` DO NOT CALL ON INSTANCE VARIABLES

