# Lists
#algo/data-structures 
#concept
**Related:**
-  [[Data Structures]]

---

## Definition
[Interface List\<E\>](https://docs.oracle.com/javase/7/docs/api/java/util/List.html)

: sequences of totally ordered collections of elements

- Can index elements

 <br/>

## Implementations
### Array
[java.util.ArrayList\<E\>](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html)

: Fixed length, contiguous block of memory

- When full $O(n)$ resize operation is run but then the space is doubled to the next few adds are $O(1)$
- Maintains current size
- Accessing(indexing) and position is easy

### Linked List
[java.util.LinkedList\<E\>](https://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html)

: Recursive data structure that is either empty (null) or a reference to a node having a generic item and a reference to a linked list

- Dynamically allocates a node for each item and attaches to the doubly-linked list via references
- Maintains a reference to the head node, tail node, and size
- Adding elements not at head requires $O(n)$ traversal

### Binary Search Tree
![[Binary Search Tree#Definition]]

![[Binary Search Tree#Runtime]]

### Runtimes

| Method           | Array                 | Linked List           |
| ---------------- | --------------------- | --------------------- |
| add(item)        | $O(1)$ amortized      | $O(1)$                |
| add(index, item) | $O(n)$                | $O(n)$                |
| get(index)       | $O(1)$                | $O(n)$                |
| indexOf(item)    | $O(n)$                | $O(n)$                |
| iterator         | iterations are $O(n)$ | iterations are $O(n)$ |
| remove(index)    | $O(n)$                | $O(n)$                |
| remove(item)     | $O(n)$                | $O(n)$                |
| size             | $O(1)$                | $O(1)$                      |

 <br/>

## List Search

: Tries to locate an item in a list

input: item(identifier, value)

output: a positive index if element is present or some designated value if not (-1, None, etc.)

- **If unordered:** must check every location using **linear search**, $O(n)$, $\varOmega(1)$
- **If ordered:** able to use **binary search** $O(logn)$, $\varOmega(1)$
- Requirements:
	- items must be comparable
	- must be able to access an arbitrary position
		- For arrays this takes $O(1)$, for linked lists it takes $O(n)$