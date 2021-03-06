# Ruby Rails
#📥 *Really needs to be reogranized*
%%
#coding 
#concept
%%
**Related:**
-  [[Ruby]]
-  [[SaaS (Software as a Service)]]
-  [[Relational Databases]]
-  [[Model-View-Controller (MVC)]]
-  [[Rails Migration]]

---

Launch server:

```Bash
# In WSL:
$ ifconfig
# get number from inet under eth0:
$ rails server -b [ip]
```

## Philosophy
- **Convention over Configuration**
	- If naming follow certain conventions, no need for config files
- **Don't Repeat Yourself (DRY)**
- **Sharp Knives are Provided**
	- Introspection and metaprogramming
	- Blocks (closures)
	- Modules (Mix-ins)

## Making an App
- A class that descends from `ActiveRecord::Base` provides methods needed to connect model to the database #📌 
- `$ exec rails g(enerate) model`
	- Default table is model name in all lowercase with an s added at the end
		- Model `Book` -> BD table `books`
		- `TimeSheet` -> `time_sheet`
	- Lets you do everything except create the table, to do that you must create a [[Rails Migration]]

### In-class
- New creates git repo, gem file
- Can

```Bash
$ gem install rails
$ rails new

Can help initally to --skip-tests --skip-javascript --skip-bundle
```

- In gem files, dependencies and their versions are lsited
- Separate groups for each env
	- Ex: in `:development, :test`, may include rspec

```Bash
$ bundle config --without production
Installs gems in every env aside from production

$ rails server launches the sesrver
launches in localhost:3000
```

- Server usually live-updates, if you change routes or server configurations you must relaunch the server 

## Structure / Design Pattern
- Uses [[Model-View-Controller (MVC)]]
	- Each Rails [[Rails Models|model]] is a resource type whose instances are rows in a particular table of a relational database 

#📌 *Just show how they relate to eachother*

### [[Rails Routing]]

### Controller actions/methods #📌 *should go in controller*
: Set instance variables which are visible to views 
- Controller methods call model's class methods ([[Ruby Rails#SQL Calls in Rails]] and any other additional methods) to retrieve database/model objects
- Routes created by `resources 'movies'` will expect to find `controllers/movies_controller.rb` what defines c`class MovieController` which descends from `ApplicationController`. This class will be expected to define `index, new, create, show, edit, update, destroy`
- Sub-directories of `views/` match controller and action names
```Ruby
# The controller
class BooksController < ApplicationController
	def index
		# Unfinished
```
- After execution, a view named `app/views/model-name/action.html.erb` will be rendered
	
#### Controller 
:eventually renders a view 
- Use `<% ... %>` to execute arbitrary lines of Ruby with no output
- Use `<%= %>` for interpolating Ruby into HTML
```HTML
<!-- The view is what is actually rendered -->
<tbody>
	<% @books.each do |book}| %>
		<tr>
			<td><%= book.title %> <!-- Ruby -->
			...
```


## [[Rails Models]]

## Debugging
### Byebug
- Adding byebug line in ruby opens interactive debugger, you can then view objects
- ⭐ Typing help give you information about what you can do

### Logger
Instead of using `puts`, use `logger`
- `logger.debug(string)`
- `logger.info(string)`
- `logger.fatal(string)`
	- Go into log directory 


### In Views
`<%= debug(@book) =%>`

## [[Javascript]] in Rails
Can link, button, form helper can take optional parameter `remote: true` to make it an [[AJAX]] request instead of HTTP 

If controller method responds to the format that is requested, to send back JS it defaults to sending `app/views/[model]/[controller name].js.erb`


```Ruby
def create
	@book = Book.create
end
```



## Testing
[[Ruby#Testing]]

## [[Aspect-Oriented Programming]]
Specify declaratively in [[Rails Models]] method

[[Rails Models#Model Validation|Validations]] add to errors hash `obj.errors`


```Ruby
validate :age_range_is_valid # custom validator method

private 
def age_range_is_valid
	if min...
			...
			
			errors
	
end



```

## Web sockets and ActionCable
Allows [[Javascript]] to create a socket to have a long-lived communication channel with any server. Rails supports web sockets through the `ActionCable` gem
- Good for things like games, chat, etc. 

## Caching 
[[DevOps#Caching]]

Caching is not turned on by default in development and test: In config/environments/development.rb, change config line 		`config.action_controller.perform_caching` to `true`

Cache method takes an optional name parameter
- Parameter is used as a key in the fragment cache  
- Think of it like a key for a Ruby Hash  
	- cache method can also take an array of items indicating a compound key  
- Example: what if we want to cache blog entries and comments, per-user?  

```HTML
%h1 #{@user.name}'s Journal'  
%ul.entries  
 - cache @user do  
	= render partial: 'entry', collection: @entries  
- content_for :sidebar do  
	- cache [@user, :recent_comments] do  
		= render partial: 'comment', collection: @recent_comments
```

Industry-strength sites configure Rails to work with memcached to offload caching into memory

### Expiring Caches
Normally don't need to 
Set an expiration time: `cache @entry, expire_in: 2.hours do`
Don’t cache for certain users: `cache_unless current_user.admin?, @entry do`
Explicitly expire a fragment by key: `expire_fragment(key)`
Expire by regex on a key: `expire_fragment(%r{@user.cache_key})` (regex match to expire anything related to user)

## Indexing
[[DevOps#Indexes]]
- `t.index(:name)`: add index to one column on table `t` in a migration  
- `t.index([:name, :age])`: add multicolumn index  
- `t.index([:name, :age], unique: true)`: add multicolumn index with a unique  
constraint  
- Use rails_indexes gem to help identify missing indices (and unnecessary ones!) 

