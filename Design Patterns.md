# Design Patterns
%%
#topic
#concept
%%
**Related:**
-  

---

#📌 Break these into different files

: Reusable structure, behavior, strategy, or technique that captures a proven solution to a collection of similar problems by separating the things that change form the things that stay the same
- Blueprint for a design

GoF (Gang of four design pattern) authors:
> - "Prefer composition and delegation over inheritance"
> - "Program to an interface, not an implementation"

==Antipattern:== Code that looks like it should follow a pattern but doesn't. Not DRY, needless repetition 


## SOLID Principles
**SOLID** OOP Design Patterns:
- **S:** [[Design Patterns#Single Responsibility Principle SRP]]
- **O:** [[Design Patterns#Open-Closed Principle OCP]]
- **L:** [[Design Patterns#Liskou Substitution Principle]] 
- **I:** [[Design Patterns#I Injection of Dependencies]]
- **D:** Demeter principle

### Single Responsibility Principle (SRP)
**Rule:** A class should have only one reason to change. Each responsibility is an axis of change, changes to one axis shouldn't affect others


**Smells:**
- High LCOM score
- Models with many sets of behaviors, large class files
- **Ex: ✏**  In a [[Rails Models]], one user model might be a customer, auth principle, social network member, etc.
	- These should be converted to separate models with 1-1 relationships 
	- You woulnd't necessarily need to build a new controller for this model 

#### LCOM (Lack of Cohesion Of Methods) score
$$\text{LCOM}_1 = 1 - \frac{\sum M(V_i)}{V*M}$$
$V$ = num instance vars
$M$ = # instance methods
$V_i$ = # instance variables used by a method (if the same 3 vars are used in 2 methods, 6)

- Should be between 0 and 1, if it's high it should be split into multiple methods

#### Address using:
- [[Design Patterns#🏘 Composition]]

###  Open-Closed Principle (OCP)
**Rule:** Code should be open for extension but not for source modification
**Smells:** 
- Switch/case statements and run-time type identification
- Can’t extend (add new types) without changing base class

#### Address using:
- [[Design Patterns#🐣 Abstract Factory Pattern]]

### Liskou Substitution Principle
**Rule:** If s is a subtype of T, the objects of type T can be replaced by objects of type S. 
If this is not the case, then it is a violation

- Not strictly about inheritance, if you can't ensure that all objects will respond the same way to an operation it is a violation
- If a depends on b but b's implementation can change, make an abstract interface that both rely on instead. Injecting dependencies 
	- **Ex: ✏**  If you use a specific service that you end up changing you'd have to rewrite all of the code that deals with the old API, instead you can write an interface for it (`AbstractMailAgent`), use that, and just change that

#### Address using:

### I: Injection of Dependencies 

#### Address using:


### D: Demeter Principle
Can call methods on yourself and your own instance variables but not the results returned by them. Object should not have details of the inner workings of another object it's manipulating

**+:** Code is more manageable and adptable 
**-:** Usually uses a lot of abstraction which can bloat classes

Friend/friend of a friend principle
```mermaid
graph LR
 a --> b
 a -. "messages okay" -.-> b
 b --> c
 a -. "messages not okay" -.-> c

```

#### Address using:

---

## Patterns 
### 🐣 Creation
#### 🐣 Abstract Factory Pattern 
==Def:== "Provide an interface for creating families of related or dependent objects  
without specifying their concrete classes"

DRYing out construction in cases where you don't know the type beforehand

#### 🐣 Singleton
==Def:== "Ensure a class has only one instance, and provide a global point of access to it"

#### 🐣 Prototype
==Def:== "Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype."

---

### 🏘Structure
#### 🏘 Composition
==Def:== "Provide operations that work on both an individual object and a collection of that type of object"

Instead of inheritance, composition is a class that has a lot of other classes that are a part of it. The main class modifies the other classes. Access a group of objects uniformly. 

```Ruby
class Report
	attr_accessor :title. :text, :formatter
	def output_report
		@formatter.output_report
	end
end
```

#### 🏘 Decorator Pattern 
(Wrapper around class and subclasses)
==Def:== "Attach additional responsibilities to an object dynamically, keeping the same interface. Helps with preferring composition or delegation over inheritance."

Subclass delegates original functionality and adds it's own. A wrapper around a class

**Ex: ✏**  [[Ruby Rails]] scopes
```Ruby
Movie.for_kids.with_good_reviews(3)
Move.has_many_fans.recently_viewed
```

#### 🏘 Facade
==Def:== "Convert the programming interface of a class into another (sometimes sim-  
pler) interface that clients expect, or decouple an abstraction’s interface from its implementation, for dependency injection or performance"

Hiding the details behind a nice interface. Isn't this the same as abstraction?
- **Con:** Can over-simplify so not usable or only make it work for one use-case

##### 🏘 Bridge
- Separating the abstraction and the implementation. So you can use several solutions for one problem
- **Con:** Can overdo it


### 🤹‍ Behavior
#### 🤹‍ Template Method Pattern (Inheritance)
==Def:== "Uniformly encapsulate multiple varying strategies for same task"
- Set of steps is the same, implementation of steps is different
- **Typical implementation:** inheritance, with sub-classes overriding abstract methods

#### 🤹‍ Strategy Pattern (Composition)
==Def:== "Uniformly encapsulate multiple varying strategies for same task"
- Task is the same, but many ways to do it
- Separating different pieces of a problem into different libraries
- Must be good default strategies
- **Typical implementation:** composition (delegation, delegate to another class to handle?)

#### 🤹‍ Null Object
==Def:== "(Doesn’t appear in GoF catalog) Provide an object with defined neutral behaviors that can be safely called, to take the place of conditionals guarding method call"

#### 🤹‍ Observer (Pub-sub)
==Def:== Allows for loose coupling between publisher (creates events) and subscriber (listens for events)

- **Con:** Can go overboard, get into event loops

#### 🤹‍ Iterator
==Def:== "Separate traversal of a data structure from operations performed on each element of the data structure"


---


Needs more info: 


#### Proxy Pattern
Implements methods as "real" service objects but intercept each call

## Client-Server
- Distinguishing clients from the server, allowing each type of program to be highly specialized
- Client: asks questions on behalf of users
- Server: wait and respond to questions, serve many clients


![[Model-View-Controller (MVC)]]

![[Active Record]]

## Peer-to-peer Architecture
- 🌎 Used in BitTorrent
- Every participant is both a client and participant


