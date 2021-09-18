# Priority Queues
#algo/data-structures 
#concept
**Related:**
-  [[Data Structures]]
- [[Heap]]
- [[03-18-2021 Huffman Coding and File Compression|Huffman Coding (good use of priority queues)]]
- [[03-18-2021 Priority Queues PSS]]

---


## Definition
[java.util.PriorityQueue\<E\>](https://docs.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html)

: Supports add and remove and orders by a specified ordering as opposed to LIFO for [[Queue]]
- Only absolutely keeps track of the next item in the sequence

**Applications**
- When you only need the lowest or highest item ordered
	- Ex: You have tasks and need to order them by due dates and only care about the next due item
- When you need to repeatedly add and remove things and need them ordered by a certain thing but only need the highest or lowest values

<br/>

## Implementations and Runtimes
- Often implemented using [[Heap]]

| Operation                 | Sorted Array                                         | Sorted Linked List | Balanced BST  | Unsorted List | ✨ **Heap**     |
| ------------------------- | ---------------------------------------------------- | ------------------ | ------------- | ------------- | ----------- |
| Insert(item, priority)    | $O(n)$ (shifting items)                              | $O(n)$             | $O(\log n)$   | $O(1)$        | $O(\log n)$ |
| Peek (highest priority)   | $O(1)$ (already at front)                            | $O(1)$             | $O(\log n)$   | $O(n)$        | $O(1)$      |
| Remove (highest priority) | $O(1)$ or $O(n)$ if highest priority must be at head | $O(1)$             | $O(\log n)$   | $O(n)$        | $O(\log n)$ |
| Create, given $n$ items   | $O(n\log n)$                                         | $O(n \log n)$      | $O(n \log n)$ | $O(n)$        | $O(n)$      |

 <br/>

## Priority Queues in Java
- Implemented as a heap using an array
- Ordered according to their natural ordering (.compare) 
	- If you don't want this, you could write your own compare method or use a [comparator object](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html) 
		- PriorityQueue\<Comparator comaparator>

![[Pasted image 20210318130404.png]]