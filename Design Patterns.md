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

## Singleton
- Can only be one of a class. Like a driver

## Facade
- Hiding the details behind a nice interface. Isn't this the same as abstraction?
- Con: Can over-simplify so not usable or only make it work for one use-case

## Bridge
- Separating the abstraction and the implementation. So you can use several solutions for one problem
- Con: Can overdo it

## Strategy
- Separating different pieces of a problem into different libraries
- Must be good default strategies

## Observer (Pub-sub)
- Allows for loose coupling between publisher (creates events) and subscriber (listens for events)
- Con: Can go overboard, get into event loops

## Client-Server
- Distinguishing clients from the server, allowing each type of program to be highly specialized
- Client: asks questions on behalf of users
- Server: wait and respond to questions, serve many clients


## Model-View-Controller (MVC)
- Goal: Separate organization of data (model) from UI and presentation (view) by introducing a controller
	- URI routes maps action to model 
- Way to organize the server application in Client-Server Architecture
==Models:== Store data about one entity 
==Controllers:== Mediate user actions requesting access to data
==Views:== Are the interface between the data and the user 
The user interacts with views and invokes controller action
- Requests come in the form of HTTP routes
- Must determine which code should be invoked to handle that route
- [[Ruby Rails]] supports MVC

## Active Record
[[Ruby Rails]]
- Rails model is a class backed by a specific table of a [[Relational Databases|RDBMS]]
	- An instance of the class is a single row
- Model has built in behaviors:
	- Create a new row in the table
	- Read an existing row into an object instance
	- Update an existing row with new attributes from a modified object instance
	- Delete row

## Peer-to-peer Architecture
- 🌎 Used in BitTorrent
- Every participant is both a client and participant


