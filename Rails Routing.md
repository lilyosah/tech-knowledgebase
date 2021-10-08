# Rails Routing
#📥 
%%
#SWE 
#concept
%%
**Related:**
-  [[Ruby Rails]]
-  

---

guides.rubyonrails.org/routing.html

: [[Ruby Rails]] routing subsystem maps incoming URLs to controller actions and extract optional parameters. By default, it adds the routes `new` and `edit`. 
- New displays what is necessary for a `create` request. 
- `edit` shows an editable version of the existing resource in preparation for `update`.
- ⭐ **Result of matching a route is calling an instance method in a controller class**
- Wildcard parameters: (e.g. `:id`) + query params are put into `params[]` hash and are accessible in controller actions

❗ Make sure each route that has a view also has a [[Rails Controllers]] action. If it has a view but not a controller action, [[Ruby Rails]] will behave as if the action exists but is empty

## Route helpers
- Route helpers decouple what the route does from the actual route URI
- Creates a whole set of routes 
	- `resources [plural model symbol or str]` 
	- Can limit with `only`
		- `resources :books, only: [:index, :show]"`
	- Can create exceptions with `except`
		- `resources :books, except: []`
	- Goes in config? #❓ 
- Create one route
	- `resource [singular model instance name]`
	- `resource :book`

*In config file*
```Ruby

Rails.application.routes.draw do
	# books is table name
	resources :books, only: [:index, :show]
end


```


### URI Helpers
Prefixes are given for each route. You can use the prefix instead of the whole path and add `_path` after
See using `$ rails routes -c [ControllerName]`
- 📝 In the table, if there is no prefix it uses the same as the above prefix

Connect to one of these routes in the [[Rails Views]] using `link_to(link text, URI path, ...config stuff)`

**Ex: ✏**  `link_to book.title, book_path(book)` *Creates link to books (prefix) route to link to individual book show pages*
**Ex: ✏**  `link_to "Go back", books_path` *Link back to books table from show page*

❕ You may have to specify the entire method bc prefixes, etc. may be shared