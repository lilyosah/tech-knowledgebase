# Rails Controllers
#📥 
%%
#topic
#concept
%%
**Related:**
-  [[Model-View-Controller (MVC)]]
	-  [[Rails Views]]

---

## Definition
The connection between [[Rails Views]] and [[Rails Models]]



> **Some** methods in controllers have a [[Rails Views]] named after them and render things, some do not
- There is a render method to show which view you want to use, but because of naming of method names in controller it will know which view to use
	- **Ex: ✏**  `def index` in controller will render view `app/views/whatever/index.html.erb`

**EVENTUALLY** something must be rendered because [[Networks|HTTP]] is request/reply protocol, but not every method corresponds to its own view
- **Ex: ✏**  You don't want to make a whole view just for create, sometimes does a redirect instead


- 📝 `params[]` is the parameters from URI, see [[Rails Routing]]

**Ex: ✏**  

```Ruby
class BooksController < ApplicationController
	# get all books from DB and make availbile in @books instance var
	def index
		@books = Book.all
	end
	
	# get one book by id and make it available to the [[Views]] through instance var @book
	def show
		begin
			@book = Book.find(params[:id])
		rescue ActiveRecord::RecordNotFound
			redirect_to books_path
		end
	end
end


```

📝 Instance methods in controllers are only retained for one call, would need to use `sessions` I think to retain them longer #📌, see [[Rails Views]]
📝 To handle exceptions, can also add `rescue_from ActiveRecord`... *not finished* at the top of a controller file 

### Naming

 |             | Case  | Convention | Number   | Example           |
 | ----------- | ----- | ---------- | -------- | ----------------- |
 | **Class**   | Upper | 🐫         | Plural   | `BooksController` |
 | **Methods** | lower | 🐍         | Singular | `sale_items`      |


## Creation
*Creates controller with open and debit [[Rails Views]]*
`bin/rails generate controller CreditCards open debit`

## Forms
![[Rails Views#Forms]]

## Validation
- You can use filters to ensure that some qualifications are met before continuing 