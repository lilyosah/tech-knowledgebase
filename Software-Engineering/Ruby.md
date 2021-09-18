# Ruby
#SWE #coding
#concept
**Related:**
-  [[Learning a new Language]]

---

#📌 Add ruby doc link
#❓ What exactly does the pound mean
#❓ double !! around something to make true/false

"Extreme object orientation"

- Everything is an object, there are no primitive types. So everything is a method call and every method returns a value
- All access to instance variables must take place via accessor methods
## Basics:
### Types, Typing, and Names
- Dynamically types
	- Interpreted/just-in-time compiled language
- Any classes can be modified at any point! Nothing is sacred
	- Requires a lot of discipline... Programs may not work the same on different computers 
- Every assignment is actually calling a method
- `false` and `nil` are falsy, **every other** value is truthy (evaluates to true)

#### Names
- Instance vars: preceded with @ (instance var) or @@ (class values)
- Vars: lower snake case is used for 
- Classes use upper camel case
- Constants: Uppercase
- Global: $ in front and then all uppercase 


### Primitives 
- No primitive types, everything is an object
	- Uses more memory but not really significant 
- `nil` signifies falsiness or a variable that refers to nothing 
- Every Ruby statement returns a value. Assignments return the value of their left hand side, the value of the var that was just assigned to. 

#### Symbols
- Symbols: immutable tokens whose value is itself `:cat`
	- Sort of like enums
- Prefixed with a colon

### Methods
Defined like
`def method_name(arg1,...)` 
and ends with end

- All return a value, if it doesn't have a return statement it **returns the last expression evaluated**
	- Most people do not specify a return statement unless you want to break at a certain point with code after it 
- **Every method is called on an object**
- You don't need parens around the method call if it doesn't result in ambiguous parsing
- Need accessor methods and mutator methods to access and change vars
- If you have a # symbol in front it means that it is called on a type
	- String#to_i

Some syntax doesn't look liek a method call but it is
Ex: 5 + 4 is equivalent to 5.send(:+, 4)

### Abstraction and Encapsulation
- Supports inheritance, `SubFoo<Foo` indicates SubFoo is a subclass of Foo
- Constructors are called as `Foo.new`, the method is called initialize 
- Class/static vars have @@, instance have @



## Methods
- `puts` print to output 
- `gets` get input
- Rocket `=>` indicated return 
- Following a method with `?` indicated that it returns true or false, part of the method name

### To
- `.to_s` to string
- `.to_sym` to symbol
- `.to_i` to integer
- `.to_f` to float
- `.to_a` to array 

### String interpolation
- Double quotes, curly braces, pound symbol outside converts it to a string
`"#{s.to_s}"`


## Data types
### Arrays
- Creation syntax is the same as in Python
- Also %w (single-quoted) syntax %W (double-quoted)
	- `%w{one two three}` --> `["one", "two", "three"]`
- .length for length
- Indexing is normal
- OOB returns `nil`
- Can contain multiple types
- `<<`, `+=` Appends
	- `my_array << nil`


### Hashes
- Two creation syntaxes
	- `w = {'a' => 1, :b => [2, 3]}`
		- Does NOT turn into symbols
	- `w = {a: 1, b: [2, 3]}` 
		- ❗ Default behavior of colon turns everything into a symbol
		- `"#{a}"` is a is a var, turns the val of a into a symbol
- `Hash#key?` checks for key

### Range object
- `a..b` inclusive range
- `a...b` exclusive range
- To create, just put in parens
	- `(1..3)`

### Strings
- `.length`
- Indexing is normal
- Constructing strings
	- `%q{}` equiv to **single quotes**: nothing inside quotes is interpolated
	- `%Q{}` equiv to **double quotes**: things are interpolated
		- Alternatively, `"#{x}flate this"`
- `a.to_f` 
	- `format("%.02f", a.to_f)`


## Basic Looping
```Ruby
3times do
	puts "Swiper no swiping!"
end
```

- For loops and while loops exist but aren't as common in ruby
- #❓ What are the pipes for?
- Calling `.each` on a collection is much more common
	- `(1..3).each {puts "Swiper no swiping"}` For one line
	- `(1..3).each do |x|`

## [[Regular Expressions]] in Ruby
> [Rubular](http://rubular.com)

`=~` operator matches a string with a regex
Ex: `"jsommers" =~ /jsommers/`
Pattern goes on the left, regex is on the right between slashes 
- Non-matching regexes return nil
- Matches return index of match, can use capture groups to show the match, prefix with $
	- `$1` returns first match 

Creation:
- `/whatever/`
- `%r{whatever}`
- `Regexp.mew('whatever', Regexp::IGNORECASE)`


## Ruby Idioms 

Poetry mode: can not use parens around method calls when it is unambiguous. Also, when the last param is a hash, you don't need curlies around the hash literal 
- `link_to "edit", :controller=<'students', :action=>'edit'`
Duck Typing: "If something looks like a duck and quacks like a duck, it might as well be a duck"
- Something responds the same way another class/type may
- ==Mix-in==: Named collection of related methods that can be added to any class what fulfills some "contract" with the methods.
	- Packed together in modules
	- Having `include ModuleName` in the class def mixes in that modules instance and class methods and variables
	- Up to the programmer to make sure that type actually has the needed requirements to mix-in the module
	
`.send` way to send methods to objects, always happens in the back-end
- `s.send(:length) # => 12`
- `s.send(:[], 0) # => 'c'`

`x||=5`: Is x is nil, assign 5

- `!` at the end of method names is destructive, modifying the original receiver

### Blocks
==Blocks==: Anonymous functions

```
arr.each do |dasjas|
	x
	x
	x
end

```

In this case you are passing in the block (a function to apply to each element) to `.each`

- `.yield` invokes the block passed to the method, passing back whatever parameter follows it 
Ex: 

```Ruby

def make_salad  
	if !block_given?  
		puts "No salad today!"  
		return  
end  
yield "lettuce" # call block passed to this method, giving param "lettuce"  
yield "tomatoes"  
yield "carrots"  
end  
make_salad { |ingredient| puts "Adding #{ingredient} to salad!" }  
# equivalently, with do/end syntax  
# make_salad do |ingredient|  
# puts "Adding #{ingredient} to salad!"  
# end  
Adding lettuce to salad!  
Adding tomatoes to salad!  
Adding carrots to salad!

```
- If you have an explicit variable that refers to a `Proc`, you call it with `.call`
	- Procs are blocks
	- `myProc.call(myParam)`
- Can also make blocks with
	- `Proc.new { |n| }`
	- `lambda` or `->` **In these cases expected to be single-line** 
		- `p = lambda { |n| }`
		- `p = ->(n) {puts n}` 

- You can check if a block was passed to a function (ex: `.each`) with `block_given?` predicate within that function
- `yield` calls the block that was passed, passes any params which go in the `|x|` spot
- Blocks have ==closures==: All variables that were in scope when the block was made are passed in with the block 
- Make no assumption about how vars are used. 
- Blocks can be explicitly captures with `&param` have to the the last param passed, in the function that they're being passed to (`.each`)
	- `each (x, &my_block)`

## Classes
- `initialize` is used to instantiate, but you call using new `thing.new`
- Still has self but it represented the class itself and not an instance of it??????? WHEN ITS ON THE DEF LINE!!!!!!!
	- Means that you call that method on the actual class and not an instance. Class method 
	- Instance of class Class, when an instance of that is the class is the class name that self is on the same line as a def within 
- When self is inside a def then it refers to an instance of the class
- Setters have `=` after method name
	- `balance=(newbal)`
- All instance vars are private, have to use pubic methods
- Shorthand for accessor methods:
	- `attr_accessor`
	- `attr_reader`
	- `attr_writer`
	- Defined like `attr_accessor :balance`
	- Accessed like `bank.balance`

Subclasses defined like
`class SavingsAccount < Account`
- Inherits all methods, variables 
- To access parents variables, use `self.balance`
- If you want to call a parents method, use `super`
	- `super.to_s`


## Iteration #📌 
- `.each` is the workhorse of Ruby, classes implement it slightly differently
	- Ex: might have key, val pairs for hash

Functional programming: methods have no side effects
### Enumerable methods
`.reject`: Loop and return a new array where the given block is not true
	- Ex: `arr.reject{|x| x < 0`: Rejects when x >= 0
`.sort`: 
`.map`: Apply the block to every element in the collection, but collects up a new array
	- Same as `.collect`?

```Ruby
y = x.map do |fruit|
	fruit.reverse
end.sort # => ["elppa"]
```

**None of these methods are defined for arrays**, Duck typing and mix-ins
- Only care that the receiver responds to `.each`
- Enumerable set of methods




## Metaprogramming

## Modules
Modules: collection of class and instance methods that aren't actually a class
One was to access things in modules explicitly `Math::sin(Math::PI/2.0)`

Alternatively, 
```Ruby
class A < B
	include myModule
end
```
inserts all instance vars, methods into class.

Method resolution:
1. Look in class first
2. Look in any included modules
3. Look in classes inherited from 
	1. These could include other modules... process may continue

Ex: Enumerable has methods like `.all?, .collect`
- Its **only** requirement is that the class implements `.each`
- Has `.sort` if the class implements `<=>`

⭐ Can check whether an objects responds to a method with `O.respond_to? :<=>` method name as a symbol

`<=>`: Comparison. a < b ==> -1, a > b ==> 1, else ==> 0

### When to use modules
- Allow reuse of **behaviors** that could conceptually apply to many different classes 
- A lot of the time, prefer composition over inheritance
==Composition==: Mixins and modules and things 


