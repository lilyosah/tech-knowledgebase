# Data Structures
Class: #algo
Week: #week/week-2 
Tags:
#algo/data-structures
#MOC
Related: 

---

# Lists
![[List#Definition]]
![[List#Runtimes]]

<br/>

# Sets
![[Set#Definition]]
![[Set#Runtime]]

<br/>

# Maps
![[Map#Definition]]
![[Map#Runtime]]

<br/>

# Stacks
![[Stack#Definition]]
![[Stack#Runtime]]

<br/>

# Queues
![[Queue#Definition]]
![[Queue#Runtime]]

<br/>

# Priority Queues
![[Priority Queue#Definition]]
![[Priority Queue#Implementations and Runtimes]]

<br/>

# Heaps
![[Heap#Definition]]
![[Heap#Runtime]]

<br/>

# Trees
![[Tree#Definition]]

<br/>

## Binary Search Trees
![[Binary Search Tree#Definition]]
![[Binary Search Tree#Runtime]]

<br/>

## Tries
![[Trie#Definition]]
![[Trie#Runtime]]


<br/>

## Graphs
![[Graphs#Definition]]

---

<br/>

# On Implementing Data Structures (Textbook 1.3)
==Generic types:== (E) allow us to define implementations that will accept any Java type.

- During the actual implementation of the class use the type parameter `<Item>` as a placeholder for whatever **concrete type** will be passed

Except ***you can't create generic arrays*** so use type casting

```java
a = (Item[]) new Object[cap];
```

==Concrete type:== the actual parameter type passed to data structures. Must be a reference type but can rely on autoboxing to convert from a primitive to reference type

==Autoboxing:== automatically converting a primitive type to reference type

**Ex:** push(17) converts 17 from int to Integer

==Wrapper types:== reference types that correspond to primitive types

- Java type parameters (`HashSet<Integer>`) must be instantiated as reference types

==Foreach loops:==


*For each transaction t in the collection, do this block of code.*

```java
for (Transaction t : collection) {
	StdOut.println(t);
}
```

- The actual iteration implementation details are hidden, the collection just needs to be iterable.

To make a structure iterable:

- Must implement an iterator() method that returns Iterator object Iterator
- Iterator class must include hasNext() and next() that return a generic item

==Bag:== unordered collection where removing items is not necessarily supported