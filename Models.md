# Models
#📥 
%%
#topic
#concept
%%
**Related:**
-  

---

Handles business logic in [[Model-View-Controller (MVC)]] architecture, 

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

## [[Rails Migration]]


### Creation Option 1
1. Create table `rails generate migration CreateBooks`
2. Apply migrations `rails db:migrate`

### Creation Option 2 (Preferred)
- `rails generate model`
- Creates a migration script along with `app/models/model.rb`
	- Can specify column names/types to generator, and the migration generator
 
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
> **So the class is empty, there are no actual instance variables, don't refer to values with `@`**
> This is why you must save after making changes to the data, otherwise the data is only in memory

### CRUDI Methods
[[Networks#Representational State Transfer REST|CRUDI]]
📝`.to_sql` method on any CRUDI method shows the corresponding SQL call at the end of any active record call

#### SELECT 
`[Model].all`
- Like `SELECT * FROM books`

#### SELECT WHERE 
`[Model].where("year >= 2000")`
- Can be chained, like
	- `[Model].where("year >= 2000").where("year <= 2020")`
	- `[Model].where("list_price < ?", 2)` interpolates `2` into `?`
	- `[Model].where("list_price < ?", "%#{match_str}%")` interpolates `match_str` into `?`
	- 📝 This does not return an array, it's an array-like thing [[Ruby#Duck typing]]
	- ❗ **Do not use regular string interpolation**, opens app up to SQL injection 
		- `[Model].where("list_price > #{min_price}")`
- `[Model].all.order_by("col")`
- `[Model].where("price < ? DESC", my_price)`

#### Create/INSERT 
`Model.create(attribute: "The Perks of being a Wallflower", year: 1999)
- If you don't specify attributes, default to `nil`/`null` (for databases)

#### Update/Read 
- `Model.find(9)` Takes ID
- To save the data in the table after making changes, save the found object with `[Model instance].save!`
	- `[Model instance].persisted?` checks if it's in the DB
- `[Model].find_by(key: "value")`
- `[Model].update_all("list_price = list_price * .9")`

#### Delete
`item.destroy`

#### Create and Save 
`item.create` (adding `!` throws exception)

#### Examples
```Ruby

class Book < ApplicationRecord
	def self.cheaper_than(val)
		Book.where("price < ?", val).orer("price")
	end
end

class Book < ApplicationRecord
	def self.price_between(lower, upper)
	end
end

```


### Computations
Do not do computations in Ruby if possible, should be done in the DB. It's much faster

**Some methods**
- `[Model].average('col')`
- `[Model].max('col')`
- `[Model].min('col')`

### Model Attributes
To change column data, `self.title.capitalize` DO NOT CALL ON INSTANCE VARIABLES

