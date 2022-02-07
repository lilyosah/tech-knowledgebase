# Rails Routing
%%
#SWE 
#concept
%%
**Related:**
-  [[Ruby Rails]]
-  

---

guides.rubyonrails.org/routing.html

: [[Ruby Rails]] routing subsystem maps incoming URLs to controller actions and extract optional parameters. By default, it adds the routes `new` and `edit`. Route helpers decouple what the route does from the actual route URI. Incoming request will match with a route which will then call the appropriate [[Rails Controllers]] action , passing any params into `params[]`
- New displays what is necessary for a `create` request. 
- `edit` shows an editable version of the existing resource in preparation for `update`.
- ⭐ **Result of matching a route is calling an instance method in a controller class**
- Wildcard parameters: (e.g. `:id`) + query params are put into `params[]` hash and are accessible in controller actions
- Specify routes in the `routes.rb` config file

❗ Make sure each route that has a view also has a [[Rails Controllers]] action. If it has a view but not a controller action, [[Ruby Rails]] will behave as if the action exists but is empty


## Route helpers
*In config file*
> Use lower 🐍 case in config file

- **Create a whole set of [[Networks#Representational State Transfer REST|CRUDI]] routes** 
	- `resources [plural model symbol or str]` 
	- Can limit to a subset with `only`
		- `resources :books, only: [:index, :show]`
	- Can create exceptions with `except`
		- `resources :books, except: []`
- **Create one route**
	- `resource [singular model instance name]`
		- **Ex: ✏**  `resource :book`
- **Root** URI route: `/` specifies the home page
	- `root to: [controller#method]`

**Ex: ✏**  In config file

```Ruby

Rails.application.routes.draw do
	# books is table name
	root 'pages#main'
	resources :books, only: [:index, :show]
end


```

**Ex: ✏**  In controller
Can do `books_path`, `book_path(book_obj)`[[]]

### URI Helpers
Prefixes are given for each route. You can use the prefix instead of the whole path and add `_path` after
See using `$ rails routes -c [ControllerName]`
- 📝 In the table, if there is no prefix it uses the same as the above prefix

Connect to one of these routes in the [[Rails Views]] using `link_to(link text, URI path, ...config stuff)`

**Ex: ✏**  `link_to book.title, book_path(book)` *Creates link to books (prefix) route to link to individual book show pages*
**Ex: ✏**  `link_to "Go back", books_path` *Link back to books table from show page*

❕ You may have to specify the entire method bc prefixes, etc. may be shared