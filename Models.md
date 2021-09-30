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

==Schema:== Collection of their tables and their structure 

 [[Design Patterns#Active Record]] 
 
 ## The Database
 - Don't destroy real user data!
	 - Rails solution: Each env has its own database, and different DB types that are appropriate for each 
	 - Development, test, production
 - Keeping env DBs consistent:
	 - ==Migration:== a script describing changes to the database #📌 *This is mentioned somewhere else*
		 - Automatable 
		 - Creates the tables

Show help: `rails g model`
### Creating Migrations
#### Option 1
1. Create table `rails generate migration CreateBooks`
2. Apply migrations `rails db:migrate`

#### Option 2
- `rails generate model`
- Creates a migration script along with `app/models/model.rb`
	- Can specify column names/types to generator, and the migration generator
 
 
### Data Types
- int, string, text, 'decimal {digits, digits}' (need single quotes around bc curly braces are special in shell), blob (raw binary)
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