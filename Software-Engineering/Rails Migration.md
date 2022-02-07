# Rails Migration
%%
#SWE 
#concept
%%
**Related:**
-  [[Ruby Rails]]
-  [[SQL]]

---

: A [[Ruby]] script describing a set of changes to make to the database schema 


## Benefits
- Do this instead of using [[SQL]] because Rails defines production environments, you'd have to make three identical [[SQL]] calls 
 - Automated == reliably repeatable
 - Can identify each migration and know which have been applied and when
	 - Often designed to be reversible 
 - Can manage with version control 

## Process
> Show help: `$ rails g model`


### 1) Creating the migration file
On command line run `$ rails g migration [migration name]` (migration name is upper 🐫 case)
In the file it generates, add your changes.

```Ruby

class CreateBooks < ActiveRecord::Migration[5.1]
	def change
		create_table books do |t|
			t.string :title
			t.decimal :price, precision: 8, scale: 2, null: false
		end
	end
end

```

### 2) Run the migration
- Run migration in development from migration file: `$ rails db:migrate`
	- 📝 It usually runs the migration in every environment, but if it doesn't you can run `$ rails db:[env]:prepare`
	- To run in production: `$ heroku run:detached rails db:migrate`
- To add to the table, have to add to the seed (that you've created!): `$ rails db:seed`

📝 If you want, you can change the column names and types, etc. before you run the migration for the first time, AFTER generating the migration file. After you run it for the first time, you would be better off scrapping the database in a low-stakes app (`$ rails db:drop`), in a higher stakes situation, use methods to change the table attribute

