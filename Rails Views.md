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
- The user interacts with views and invokes [[Rails Controllers]] action
	- One [[Rails Controllers]] may have several views
- Found in `app/views/[plural lowercase model]/index.html.erb`

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

## Forms
- [[HTML]] forms allow collection of data from the user
- [[Ruby Rails]] defines a `new` action and route to use this data in a `create` or `update` call
	- `GET /movies/new` names the action, the helper `new_movie_path` generates the URI portion of the route
	- Action is handled by the method `MoviesController#new`
	- By default, the [[Rails Controllers]] action will end by rendering a view `app/views/movies/new.html.erb`
- This would need the controller to have some idea of what the form field names are. [[Ruby Rails]] uses tag helper methods that generate [[HTML]] form tags whose names follow particular conventions that make them easy to parse by the controller action

### Helpers
You don't have to use form tag helpers to submit data from forms but it makes things easier 

`form_tag` helper takes two arguments
- URI to which the form should submit (EX: RESTful Route helper)
- Hash of optional arguments, one of which may be the HTTP method that should be used to submit the form

Ex for Product:
*products_path is the name of the route helper*
`<%= form_tag products_path, :method => :post do %>`

- `params['movie']` is a hash of movie attribute names and values that can be passed directly to `Movie.create!(params['movie'])`
	- [[Rails Controllers]] action can inspect `params[]`
		- Like `params[:query]`

Ex in controller: #📌  Move to controller somehow

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


- When creating or updating a model, for user friendliness it's common to 	`redirect_to` a view such as `index` rather than rendering a dedicated view
`flash[]`: special object that quacks like a hash but whose contents only persist from the current request to the next
- If you put something in flash during a controller action, you can only access it during the very next action
- `flash[:notice]` is used for info messages
- `flash[:alert]` is used for messages about things going wrong
`session[]` is used to persist contents "forever" across requests from the same browser



