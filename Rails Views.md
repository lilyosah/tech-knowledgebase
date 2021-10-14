# Rails Views
#📥 
%%
#SWE 
#coding 
#concept
%%
**Related:**
- [[Design Patterns]] 
- [[Model-View-Controller (MVC)]]
	- [[Rails Controllers]]
	- [[Rails Models]]

---
 
 ## Definition
 The interface between the data and the user in [[Model-View-Controller (MVC)]] architecture. 
- The user interacts with views and invokes [[Rails Controllers]] actions
	- One [[Rails Controllers]] may have several views, named after the controller methods
- Found in `app/views/[plural lowercase model]/index.html.erb`


❗ Make sure to not do too much code here, it should be handled in the [[Rails Controllers]]
#📌  *Add bit about which one interpolates and which does not show result of code*



**Ex: ✏**   

```HTML
<!-- views/whatever/index -->
<h1>Books index</h1>
<p>
	<%= @books.inspect %>
</p>

<table>
	<tr>
		<th>Title</th>
		<th>Pages</th>
		<th>Year</th>
	</tr>
	<% @books.each do |book| %>
		<tr>
			<td><%= book.title %></td>
			<td><%= book.pages %></td>
			<td class="price"><%= book.year %></td>
		</tr>
	<% end %>
</table>
		
```


### Naming

| Case  | Convention | Number | Example           |
| ----- | ---------- | ------ | ----------------- |
| Lower | #❓         | Singular | `show.html.erb` |

## Partials?
- Blocks exist in views and render more of the page?

## Linking Views
Use [[Rails Routing#URI Helpers]]


## Forms
- [[HTML]] forms allow collection of data from the user
- [[Ruby Rails]] defines a `new` action and route to use this data in a `create` or `update` call
	- `GET /movies/new` names the action, the helper `new_movie_path` generates the URI portion of the route
	- Action is handled by the method `MoviesController#new`
	- By default, the [[Rails Controllers]] action will end by rendering a view `app/views/movies/new.html.erb`
- This would need the controller to have some idea of what the form field names are. [[Ruby Rails]] uses tag helper methods that generate [[HTML]] form tags whose names follow particular conventions that make them easy to parse by the controller action

### Helpers
You don't have to use form tag helpers to submit data from forms but it makes things easier 

#### form_with
✨ Go-to form helper

**Arguments:**
- `local`: for regular URIs, must specify local is true. Otherwise, makes an AJAX call

**Ex: ✏**  For Books
*View*
```HTML
<!-- 
You don't need to specify the URI path to controller but you can if you want -->

<%= form_with model: @book, (method: post,) local: true do |book_form %>
	<%= book_forn.label :title %>
		...


```

*In controller*
```Ruby
def new 
	@book = book.new
end

def edit
	@book = Book.find params[:id]
	@book.update(create_params)
	flash[:notice]
	#📌 
end

def destroy
	@book = Book.find params[:id]
	book.destroy
	flash[:notice] = "book '#{@book.title}' deleted."
	redirect_to books_path
end
```


#### form_tag
❗ **form_with is easier most of the time if you have a clear model you want it to relate to**
- Use `form_tag` if you don't have a clear model
	- **Ex: ✏**  A search form

**Arguments:**
- URI to which the form should submit (EX: RESTful Route helper)
- Hash of optional arguments, one of which may be the HTTP method that should be used to submit the form

**Ex: ✏**   for Product:
*products_path is the name of the route helper*
`<%= form_tag products_path, :method => :post do %>`

- `params['movie']` is a hash of movie attribute names and values that can be passed directly to `Movie.create!(params['movie'])`
	- [[Rails Controllers]] action can inspect `params[]`
		- Like `params[:query]`

Code using `params` in [[Rails Controllers]]

```Ruby
class BookController < ApplicationController
	def index
		@books = Book.all
		if params[:query]
			@books = @books.where("title LIKE ?", "%#{params[:query]}")
		end
	end
end
```


## Saving Data
### Redirecting
- When creating or updating a model, for user friendliness it's common to 	`redirect_to` a view such as `index` rather than rendering a dedicated view
	- Annotates a response object so it know's what to show?
- ❗ This does not return from the controller method, it continues to execute
- ❗ If you redirect more than once, you'll get a multiple render error
	- So you can do something like `redirect_to books_path and return`
- ⭐ If there is an error after rendering a template, you still have to return that rendered view to the browser

### Flash
`flash[]`: special object that quacks like a hash but whose contents only persist from the current request to the next
- If you put something in flash during a controller action, you can only access it during the very next action
- `flash[:notice]` is used for info messages
- `flash[:alert]` is used for messages about things going wrong
	- **Ex: ✏**   Save failed, fix yr stuff

```Ruby

def create
	b = Book.new(:book) # mass assignment of attributes
	if b.save # If save succeeds
		flash[:notice] = "Saved!"
		redirect_to book_path(b)
	else # If save fails
		flash[:warning] = "Book couldn't be created"
		redirect_to new_book_path
end
	
```

This will fail! Ruby does not allow mass assignment of attributes. Use `require` and `permit` methods on params
- `require`: verify that expected info is present
- `permit`: permit particular info

Better:
```Ruby

def create
	b = Book.new(create_params)
	if b.save # If save succeeds
		flash[:notice] = "Saved!"
		redirect_to book_path(b)
	else # If save fails
		flash[:warning] = "Book couldn't be created"
		redirect_to new_book_path
end
	
private
	
def create_params
	params.require(:book).permit(:title, :publisher, :year, :list_price, :pages)
	
end
	
```

*Getting the flash messages to show*
- To put them (redners of flash messages) all in one place, add in `app/views/layouts/application.html.erb`

```HTML

<% if flash[:notice] %>
	<div>
		??? #📌 add this code
	</div>


```

### Session
`session[]` is used to persist contents "forever" across requests from the same browser. Like a hash
	- ❗ Do not over-stuff `session[]`! Because it is made into a cookie with a limited size - backed by cookies

This is how you track people... 
`reset_session` empties session
`session.delete(:some_key)` removes some key

### Cookies
Behaves the same as `session` 
- Can be a separate thing
- Can only contain up to 4 KiB limit
