# Rails Migration
#📥 
%%
#SWE 
#concept
%%
**Related:**
-  [[Ruby Rails]]
-  [[SQL]]

---

: A [[Ruby]] script describing a set of changes to make to the database schema 
- Do this instead of using [[SQL]] because Rails defines production environments, you'd have to make three identical [[SQL]] calls 
 - Automatable 
- `$ exec rails g(enerate) migration [migration name]`
- To add to the table, have to add to the seed

Show help: `rails g model`

## Creating the table
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