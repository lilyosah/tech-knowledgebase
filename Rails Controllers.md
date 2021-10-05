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
- There is a render method to show which view you want to use, but bc of naming o

**Ex: ✏**  

```Ruby
class BooksController < ApplicationController
	# get all books from DB and make availbile in @books instance var
	def index
		@books = Book.all
	end
	
	# get one book by id and make it available to the [[Views]] through instance var @book
	def show
		@book = Book.find(params[:id])
	end
end


```


## Creation
*Creates controller with open and debit [[Rails Views]]*
`bin/rails generate controller CreditCards open debit`
