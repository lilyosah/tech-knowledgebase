# Ruby
#SWE #coding
#concept
**Related:**
-  [[Learning a new Language]]

---

#❓ What exactly does the pound mean

## Resources
- [Ruby Doc](https://ruby-doc.org/core-3.0.2/doc/syntax_rdoc.html)
- [Rubular (Regex)](https://rubular.com/

## Basics
"Extreme object orientation"

- Everything is an object, there are no primitive types. So **everything** is a method call and **every method returns a value**
- All access to instance variables must take place via accessor methods

### Types, Typing, and Names
- Dynamically typed
	- Interpreted/just-in-time compiled language
- Any classes can be modified at any point! Nothing is sacred 😭
	- Requires a lot of discipline... Programs may not work the same on different computers 
- `false` and `nil` are falsy, **every other** value is truthy (evaluates to true)
- Every Ruby statement returns a value. Assignments return the value of their left hand side, the value of the var that was just assigned to. 

#### Naming
Instance vars: preceded by `@` 
Class vars: preceded by `@@`

##### Case
Vars: lower snake case 
Classes: upper camel case
Constants: Uppercase
Global: `$` in front and then all uppercase 

### Primitives 
- ⭐ No primitive types, everything is an object
	- This does use more memory but not really a significant amount 
- `nil` signifies falsiness or a var that refers to nothing 

#### Symbols
==Symbols:== immutable tokens whose value is itself 
- Prefixed with a colon `:`
	- Ex: `:cat`
- Sort of like enums

### Abstraction and Encapsulation
- Supports inheritance, `SubFoo<Foo` indicates `SubFoo` is a subclass of `Foo`
- Constructors are called as `Foo.new`, the method in the class body is called `def initialize()` 

### Iteration

```Ruby
3times do
	puts "Swiper no swiping!"
end
```

- For loops and while loops exist but aren't as common in Ruby
- Calling `.each` on a collection is much more common, it's the workhorse of Ruby, classes may implement it slightly differently
	- Ex: might have key, val pairs for hash
	- `(1..3).each {puts "Swiper no swiping"}` For one line
	- `(1..3).each do |x|`
		- The variable in pipes is the value returned by the iterator


## Methods
Defined like
`def method_name(arg1,...)` 
and ends with `end`

- **All return a value,** if it doesn't have a return statement it **returns the last expression evaluated**
	- Most people do not specify a return statement unless you want to break at a certain point with code after it 
- **Every method is called on an object**
	- Even if it doesn't look like a method call, it is.
	- Ex: `5 + 4` is equivalent to `5.send(:+, 4)`
	- `.send` sends methods to objects it always happens in the back-end
		- Method names are sent as symbols
		- `s.send(:length) # => 12`
		- `s.send(:[], 0) # => 'c'`
- You don't need parentheses around the method call if it doesn't result in ambiguous parsing
- Need accessor and mutator methods to access and change vars, cannot be done without methods

### Naming %%%%Conventions
- If you have a `#` symbol in front, it specifies that the methods is called on a certain class
	- ex: `String#to_i`
- Following a method name with `?` indicates that it returns true or false
	- Ex: `.has_money?`
- Following a method name with `!` indicates that it is destructive and modifies the original receiver, otherwise you can assume that it returns a new object

### Useful Methods
- `puts` print to output 
- `gets` get input

#### Conversion
- `.to_s` to string
- `.to_sym` to symbol
- `.to_i` to integer
- `.to_f` to float
- `.to_a` to array 

#### String interpolation
- Double quotes with pound symbol before curlies interpolates vars in a string
	- Ex: `"Hello, #{name.to_s}"`


## Classes
- `initialize` is used to instantiate, but you call using new `Thing.new`

### Self
- **WHEN ON A METHOD DEF LINE:** Represents the class itself and not an instance of it 
	- Means that you call that method on the actual class and not an instance. Class method 
	- Instance of class `Class`, when an instance of that is the class is the class name that self is on the same line as a def within #❓ *I have no idea what I was trying to say here*
- **WHEN INSIDE A METHOD:** Refers to the particular instance of the class

### Subclasses
Subclasses defined like
`class SavingsAccount < Account`
- Inherits all methods, variables 
- To access parents variables, use `self.balance`
- If you want to call a parents method, use `super`
	- `super.to_s`

### Defining Methods
- Setters have `=` after method name
	- `balance=(newbal)`
- All instance vars are private, must use accessor methods to change/read
- Shorthand for accessor methods:
	- `attr_accessor`: read & write
	- `attr_reader`: only read
	- `attr_writer`: only change?
	- Defined like `attr_accessor :balance` (the instance var is referred to by a symbol of its name)
	- After vars have accessor methods they're accessed like `bank.balance`

==Functional programming:== methods have no side effects
## Data Structures
### Arrays
Creation:
- Same as [[Python]] syntax
	- Also has `%w` (single-quoted),  `%W` (double-quoted) creation syntax
		- `%w{one two three}` => `['one', 'two', 'three']`

Other
-   `.length` for length
- Indexing is normal
	- `my_array[0]`
- OOB returns `nil`
- May contain multiple types
- `<<`, `+=` Appends
	- `my_array << nil`

### Hashes
Like dictionaries in python, or a Java [[Map]]

Creation:
	1. `w = {'a' => 1, :b => [2, 3]}`
		- Does NOT turn the keys into symbols
	2. `w = {a: 1, b: [2, 3]}` 
		- ❗ Default behavior of colon turns everything into a symbol
		- `"#{a}"` if `a` is a var, turns the val of `a` into a symbol

Other
- `Hash#key?` checks for key

### Range object
Creation:
- just put in parentheses
- `(1..3)`

Other
- `a..b` inclusive range
- `a...b` exclusive range

### Strings
Creation:
- `%q{}` equiv to **single quotes**: nothing inside quotes is interpolated
- `%Q{}` equiv to **double quotes**: things are interpolated, *I believe this also lets the string span multiple lines?*
	- Alternatively, `"#{x}flate this"`

Other
- `.length`
- Normal indexing
- `a.to_f` 
	- `format("%.02f", a.to_f)`


## [[Regular Expressions]] in Ruby

`=~` operator matches a string with a regex
Ex: `"jsommers" =~ /jsommers/`
Pattern on the left, regex on the right between slashes 
- Non-matching regexes return `nil`
- Matches return index of match, can use capture groups to show the match, prefix with `$`
	- `$1` returns first match 

Creation:
- `/whatever/`
- `%r{whatever}`
- `Regexp.mew('whatever', Regexp::IGNORECASE)`


## Ruby Idioms 
==Idioms:== specific to this language

### Poetry mode
Including parentheses after method calls is optional when it is unambiguous.
- Ex: `puts "hello!"`

Also, when the last parameter passed is a [[Ruby#Hashes|Hash]], you don't need curlies around the hash literal 
- Ex: `link_to "edit", :controller=<'students', :action=>'edit'`

### Duck typing
> "If something looks like a duck and quacks like a duck, it might as well be a duck"

If one class behaves the same way as another, it can be used in the same context as the other, who cares about it's "guts". Suitability for a certain use-case is determined by whether or not the class implements required methods. If the class **does** meet certain requirements, for example, implementing `.each`, then it may mix-in a set of other behaviors.

==Mix-ins:== Named collections of related methods that can be added to any class that fulfills some "contract" with the methods.
	- Ex: if a class implements `.each`, then it may include [Enumerable](https://ruby-doc.org/core-3.0.2/Enumerable.html)
	- Packed together in modules
	- Having `include ModuleName` right under the class definition **mixes in that modules instance and class methods and variables**
	- It is to the programmer to make sure that type actually has the needed requirements to mix-in the module

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
- You can check if a block was passed to a function (ex: `.each`) with the `block_given?` predicate within that function
- Blocks have ==closures==: All variables that were in scope when the block was made are passed in with the block 
- **Make no assumption about how vars are used**
- Blocks can be explicitly captured with `&param_name`. This must be the the last param passed, in the function that they're being passed to (`.each`)
	- This is useful in case you want to write a method that takes a block and if it needs to pass it to another method, among other situations
	- `each (x, &my_block)`

####  Yield
`.yield` **invokes the block passed to the method,** passing back whatever parameter follows it into the var(s) surrounded by pipes in the block call

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

#### Procs
Procs are just blocks
- If you have an explicit variable that refers to a `Proc`, you call it with `.call`
	- `myProc.call(myParam)`
- Can also make blocks with
	- `Proc.new { |n| }`
	- `lambda` or `->` **(In these cases, the block is expected to be single-line)** 
		- `p = lambda { |n| }`
		- `p = ->(n) {puts n}` 

### Modules
==Modules:== collection of class and instance methods that aren't actually a class
One was to access things in modules explicitly `Math::sin(Math::PI/2.0)`

Alternatively, 
```Ruby
class A < B
	include myModule
end
```
inserts all instance vars, methods into class.

Method resolution order:
1. Look in that class first
2. Look in any included modules
3. Look in classes inherited from 
	1. These could include other modules... process may continue

Ex: Enumerable has methods like `.all?, .collect`
- Its **only** requirement is that the class implements `.each`

⭐ Can check whether an objects responds to a method with `O.respond_to? :<=>` method name as a symbol

#### When to use modules
- Allow reuse of **behaviors** that could conceptually apply to many different classes 
- A lot of the time, prefer composition over inheritance
==Composition==: Mixins and modules and things 

#### Enumerable module methods
- `.reject`: Loop and return a new array where the given block is not true
	- Ex: `arr.reject{|x| x < 0`: Rejects when x >= 0
- `.sort`: Requires that the class implements `<=>`
	- `<=>`: Comparison. a < b ==> -1, a > b ==> 1, else ==> 0
- `.map`: Apply the block to every element in the collection, but collects up a new array
	- Same as `.collect`

```Ruby
y = x.map do |fruit|
	fruit.reverse
end.sort # => ["elppa"]
```

**None of these methods are defined for arrays** because the array mixes in enumerable
- Only care that the receiver responds to `.each`


### Open Classes and Modules
- All classes are open in Ruby, can be overridden/changed
- This can be kind of dangerous 

**Ex: ✏**  Can override numeric and add classes, etc.
- `method_missing`: invoked on an object doesn't know how to handle a particular method call
	- Always takes `method_sym` argument but doesn't have to be called that
	- 📝 `respond_to?` would NOT recognize methods being accepted through method missing

```Ruby
class Numeric 
	def method_missing(method_sym, *args) # This sucks up all other args
		method_name = mehtod_sym.to_s
		if method_name =~ /^meters?$/
			self
		if method_name =~ /^centimeters?$/
			self * 0.01
		else
			super method_sym, *args # This unpacks all other args
		end
	end
end

```

In this case, the parent may also have a `method_missing` that we don't want to break


### Other interesting things
- double `!!` in front of something to make true/false
	- Ex: `!!balance` if `balance` is `nil`, will be `false`
- `x||=5`: If `x` is `nil`, assign 5

## Meta-programming
: Code generates new code at runtime

- Write code as a string and pass to `class_eval`, `instance_eval`, `module_eval`
- Code gets executed in its specific context
	- ❗ class and instance meanings are kind of reversed here
	- `instance_eval` to add class/static methods
	- `class_eval` to add instance
	- `module_eval` to add to modules, **not** class

**Ex: ✏**  
```Ruby
def new_conversion_factor (name, factor)
	code = %Q{def #{name}; self * #{factor}; end}
	Numeric.module_eval(code)
end

def getset(sym)
	name = sym.to_s
	getter = %Q{def #{name}; @
end
```





## Testing
[[Testing]] in Ruby uses the RSpec test framework

- Tests are under `spec/` folder
- Test files are in Ruby and should require the Rspec library `require 'rspec'`
- `it` method describes what the test does

```Ruby
require 'rspec-example'
require 'rspec'

describe "RSpec-example" do
	context "sum tests" do
		it "should work correctly with an empty array" do
			expect(sum([]).to eq(0))
		end
		it "should work correctly with an array of 1 element" do
			expect(sum([S]).to eq(S))
		end
	context "tuesday? tests" do
		# t is a time mock object
		t = double("time")
		expect(t).to receive(:wday).and_return(2)
		expect(Time).to receive(:now).and_return(t)
		expect(tuesday?).to be_truthy
end
```

- When running, need to specify where the tests are

```Bash 
$ rspec -I. spec/rspec_example_spec.rb
```

