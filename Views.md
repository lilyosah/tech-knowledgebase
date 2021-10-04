# Views
#📥 
%%
#topic
#concept
%%
**Related:**
- [[Design Patterns]] 
- [[Model-View-Controller (MVC)]]

---
 
 ## Definition
 The interface between the data and the user in [[Model-View-Controller (MVC)]] architecture. 
- The user interacts with views and invokes controller action

## Forms
- [[HTML]] forms allow collection of data from the user
- [[Ruby Rails]] defines a `new` action and route to use this data in a `create` or `update` call
	- `GET /movies/new` names the action, the helper `new_movie_path` generates the URI portion of the route
	- Action is handled by the method `MoviesController#new`
	- By default, the [[Controllers]] action will end by rendering a view `app/views/movies/new.html.erb`
- This would need the controller to have some idea of what the form field names are. [[Ruby Rails]] uses tag helper methods that generate [[HTML]] form tags whose names follow particular conventions that make them easy to parse by the controller action

### Helpers
`form_tag` helper takes two arguments
- URI to which the form should submit (EX: RESTful Route helper)
- Hash of optional arguments, one of which may be the HTTP method that should be used to submit the form

