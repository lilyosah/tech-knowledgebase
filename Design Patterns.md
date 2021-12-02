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

==Antipattern:== Code that looks like it should follow a pattern but doesn't. Not DRY, needless repetition 


## SOLID Principles
**SOLID** OOP Design Patterns:
- **S:** Single responsibility principle (per class) (SRP)
- **O:** Open-closed principle (OCP)
- **L:** Liskou substitution principle 
- **I:** Injection of dependencies
- **D:** Demeter principle

### SRP
Rule: A class should have only one reason to change
- Each responsibility is an axis of change, changes to one axis shouldn't affect others
- Ex: In a [[Rails Models]], one user model might be a customer, auth principle, social network member, etc.
	- These should be converted to separate models with 1-1 relationships 

Lack of cohesion of methods: LCOM score
- Should be between 0 and 1, if it's high it should be split into multiple methods

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


![[Model-View-Controller (MVC)]]

![[Active Record]]

## Peer-to-peer Architecture
- 🌎 Used in BitTorrent
- Every participant is both a client and participant


