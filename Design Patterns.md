# Design Patterns
%%
#topic
#concept
%%
**Related:**
-  

---

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

## Peer-to-peer Architecture
- 🌎 Used in BitTorrent
- Every participant is both a client and participant
