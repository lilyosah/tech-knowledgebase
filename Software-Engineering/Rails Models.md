``# Rails Models
%%
#SWE
#coding 
#concept
%%
**Related:**
-  [[Rails Views]]
-  [[Model-View-Controller (MVC)]]
-  [[Rails Migration]]

---

## Definition
Handles business logic in [[Model-View-Controller (MVC)]] architecture. A model class corresponds to a table where each row is one instance of the table. 
Inherits from [[Active Record]] which provides abstracted CRUDI methods for relational databases.

- 1 [[Relational Databases|Relational Database]] table = 1 model class
	- **Naming:** snake-case and plural
	- **Ex:** `books` table, `time_cards`
- 1 row = 1 model instance
	- **Naming:** Upper-camel-case and singular
	- **Ex:** `Book` class, `TimeCard`
	- Found in 	`app/models/book.rb`
- Each row has a unique primary key, automatically assigned by Rails
	- By convention, and integer called `id`

- `[Model].new` creates new model instance, but this does NOT save it. You need to do `save` after to actually save it, or just do `create` instead of the two step process. 

==Schema:== Collection of their tables and their structure 


### Model Naming
 - singular, upper-camel-case

| Case  | Convention | Number   | Case  | Example          |
| ----- | ---------- | -------- | ----- | ---------------- |
| Upper | 🐫         | Singular | Upper | `RentalProperty` |

 
 ## The Database
 - Don't destroy real user data!
	 - Rails solution: Each env has its own database, and different DB types that are appropriate for each 
	 - Development, test, production
 - ❗ Use [[Rails Migration]]s to keep the DB consistent, do not just manually edit the DB!

### Database Naming
| Case  | Convention | Number | Case  | Example             |
| ----- | ---------- | ------ | ----- | ------------------- |
| Upper | 🐍         | Plural | lower | `rental_properties` |

### Creation
####  Option 1
![[Rails Migration#Process]]

#### Option 2 (Preferred)
- `$ rails generate model`
- Creates a migration script along with `app/models/model.rb`
	- Can specify column names/types to generator, and the migration generator
 
 ### Associations
 [[Relational Databases#Associations and Foreign Keys]]
 Declare in model classes that are pointed to in other DBs:
 
 ```Ruby
class Review < ActiveRecord ::Base  
	belongs_to :movie
	belongs_to :moviegoer
end

# In Movie and Moviegoer:
has_many :reviews

```
 
 - Doing this will give many helper methods to traverse and use associations.
 - If something `belongs_to` something, it has to specify which book it belongs to before saving
 - Foreign keys must be named after `[owning obj. singular]_id`
	 - **Ex: ✏**  `book_id`

#### Association methods
- `find`:  find object by ID
- `select`: select specific attribute from owned objects
- `minumum`, `maximum`, `average`, `sum`: same methods avail on `ActiveRecord` objects

**Ex: ✏**  
```Ruby
b = Book.find(1)
b.reviews.find(1)
b.reviews.select(:stars)
b.reviews.maximum(:stars)
```

#### Adding owned objects using owner
- `create`, `new`, `build`, `<<` method on owning object

#### One-to-one associations
Owning: `has_one`
Owned: `belongs_to`

 #### One-to-many associations
 📝 If you don't include both `has` and `belongs` in the correct place, you could still go from one with the correct relation to the other, but not the other way
 
1. Add `has_many` to owning class
2. Add `belongs_to` to the owned class
 	- Creates a foreign key in the belongs_to DB
```Ruby 
class Book < ApplicationRecord  
	has_many :reviews  
	# this is the "owning" class  
end  

class Review < ApplicationRecord  
	belongs_to :book  
	# this is the "owned" class  
	# the foreign key goes here  
end

```
1. Create a DB migration to add the foreign key to the owned table if it doesn't already exist 
	- With `t.references :book, foreign_key: true` in migration file if you didn't specify via command line
 
 #### Many-to-many
 Has two flavors: Through relations and join tables.
 
 **Ex: ✏**  
 
 ```mermaid
graph LR
 Author <-- M - M --> Book
 Book <-- 1 - M --> R[Review: review_author_id, book_id]
 RA[Review Author: user_id] <-- 1 - M --> R
 User <-- 1 - 1 --> RA
 
```

  ##### Through Relations
Connecting two indirectly related DBs. Say that it has many of the third table and specify which column it should go through. Probably has something else meaningful in this table to say about connecting the data. Otherwise, you can use a join table.

> "When two models A and B each have a has-one or has-many relationship to a common third model C, a many-to-many association between A and B can be established through C."

**Ex: ✏**  

```Ruby
class Review < ApplicationRecord 
	has_many :reviews
	has_many :books, through: :reviews
	belongs_to :user
end
```

###### Add to routes
Will add nested CRUDI under books route.
**Ex: ✏**   `/books/:book_id/reviews/post`
```Ruby
resources :books do
	resources :reviews
end

```

 ##### Has-and-belongs-to-many (HABTM) (Join tables)
 A different way to implement many-to-many, largely superceded by `has_many: through` but if the middle table doesn't have any meaningful attributes you may want to use this
 - Uses a join table
 
###### Join tables
- A third table that only stores foreign keys of the two other tables, doesn't say anything about the data other than that they are related
- Contains two foreign keys which map to IDs in the two tables it joins
- **Naming:** lower, plural of each model in alpha order

**Ex: ✏**  
Genre: `has_and_belongs_to_many: books`
Book: `has_and_belongs_to_many: genres`
Join table of `Genre` + `books` = `books_genres` join table which has keys `book_id`, `genre_id`

**Ex: ✏**  
For pizza and toppings, 
`pizzas_toppings` join table with `pizza_id` and `topping_id`

Table may look like 

| P_id | t_id |
| ---- | ---- |
| 1    | 1    |
| 1    | 2    |

To specify that one pizza has two toppings

#### Scopes
Can define `has_many` and `has_one` scopes

```Ruby
class Book < ActiveRecord::Base
	has_many :best_reviews -> {where('stars = 5')}
	has_many :best_reviews -> {Book.joins(:authos).where('authors.dod is NULL')}
		...
		
		
end
```
 
## Data Types
`integer`, `string`, `text`, `'decimal {digits, digits}', references` (need single quotes around decimal because curly braces are special in shell), `blob` (raw binary)
📝 Can't have array 
 
**Ex: ✏ Model for a product and user**  
Model for a product:
- `integer` ID
- `integer` Quantity
- `string` Image URL
- `string` Name
- `decimal` Price
- `text` Description
- `string` Manufacturer, maybe in another model
- `string` Category/tags - probably in another model
- Reviews - probably in another model
- `reference`


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
- These are provided when descending from [[Design Patterns#Active Record]] 
>📝 Can do `[Model].methods` to see massive list of methods
- This is great because if different databases are used for each environment you don't need to change your code


> ⭐ The getters and setters do not modify instance variables, it's data in the db table.
> **So the class is empty, there are no actual instance variables, don't refer to values with `@`**, use 
> This is why you must save after making changes to the data, otherwise the data is only in memory

### CRUDI Methods
[[Networks#Representational State Transfer REST|CRUDI]]
> 📝`.to_sql` method on any CRUDI method shows the corresponding SQL call at the end of any active record call

📝 Use the model class name to search through the entire table
**Ex: ✏**  `RentalProperty.find(id)`

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
		- Bad!: `[Model].where("list_price > #{min_price}")`

#### Create/INSERT 
`Model.create(attribute: "The Perks of being a Wallflower", year: 1999)`
- If you don't specify attributes, default to `nil`/`null` (for databases)

#### Update/Read 
- `Model.find(9)` Takes ID
- To save the data in the table after making changes, save the found object with `[Model instance].save!`
	- `[Model instance].persisted?` checks if it's in the DB
- `[Model].find_by(key: "value")`
- `[Model].update_all("list_price = list_price * .9")`

#### Order
`[Model].all.order_by("col")`

#### Delete
`item.destroy`

#### Create and Save 
`item.create` (adding `!` throws exception)

### Examples
```Ruby

# Get books cheaper than a given value
class Book < ApplicationRecord
	def self.cheaper_than(val)
		# query the whole table
		Book.where("price < ?", val).order("price ASC") # order by ascending price
	end
end

# Get books in-between two given values in descending order
class Book < ApplicationRecord
	def self.price_between(lower, upper)
		Book.where('price > ?', lower).where('price < ?', lower).order('price DESC')
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

## Model Validation
: used to verify that inputs are valid
- Add `validates :field, whatever_method: true` at the top of the model class
- Validation errors are returned in `ActiveModel::Errors` object returned by `errors`
- Lots of helper methods are built in to rails, look up `ActiveRecord` validations to see

> ❗ You need to do do both server side AND form validation (when you specify the type of input [[Rails Views#Forms]]) because someone could try to post garbage directly to the DB using the URL and not the form


You can also specify that custom code should be injected at a certain point [[Aspect-Oriented Programming]]

```Ruby
after_save :my_method


def my_method
	# code!
end
```


## Scopes 	#📌 
: pre-defined queries that are lazily evaluated
- Reusable
- Obviates the need to define a lot of class methods on models
- Can set  default scope to apply to all queries
	- `default_scope {order('name')}`
	- If you need to avoid default, use `unscoped` method
		- `Product.unscoped`
- Can be chained
	- `Product.min_age(0).max_age()`
- Lazily evaluated: query is not executed until you try to iterate the resulting Enumerable
- ✨ Use `to_sql` method to dump query code from a complicated stacked query for debugging

**Ex: ✏**  
```Ruby
scope :scopename, -> { query_fragment }
# With param
scope :scopename, ->(parm) { query_fragment using param }
```

```Ruby
class Product < ApplicationRecord 
	scope :for_infants, -> {where('...')}


```