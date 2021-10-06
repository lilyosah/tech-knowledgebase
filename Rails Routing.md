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
	resources :books, only: [:index, :show]
end


```
