# Routing
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

- Rails routing subsystem maps HTTP routes to code in the app that performs the correct action
- Adds default routes `new` and `edit`. New displays what is necessary for a `create` request. `edit` shows an editable version of the existing resource in preparation for `update`.
- Route helpers decouple what the route does from the actual route URI
- `resources [plural model sylbol or str]` creates whole set of routes
	- `resources :books, only: [:index, :show]"`
	- Goes in config? #❓ 

## Routes
: Map incoming URLs to controller actions and extract optional parameters 
- Result of matching a route is calling an instance method in a controller class
- Wildcard parameters: (e.g. `:id`) + query params are put into `params[]` hash and are accessible in controller actions