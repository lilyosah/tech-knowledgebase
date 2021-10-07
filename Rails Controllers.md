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

`params[]` is the parameters from URI, see [[Rails Routing]]
- There is a render method to show which view you want to use, but bc of naming of method names in controller it will know which view to use
	- Ex: `def index` in controller will render view `app/views/whatever/index.html.erb`
- Each method in controller has a [[Rails Views]] named after it?

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


📝 To handle exceptions, can also add `rescue_from AcriveRecord`... *not finished* at the top of a controller file 

### Naming

 |             | Case  | Convention | Number | Example           |
 | ----------- | ----- | ---------- | ------ | ----------------- |
 | **Class**   | Upper | 🐫         | Plural | `BooksController` |
 | **Methods** | lower | 🐍         |        |                   |


## Creation
*Creates controller with open and debit [[Rails Views]]*
`bin/rails generate controller CreditCards open debit`
