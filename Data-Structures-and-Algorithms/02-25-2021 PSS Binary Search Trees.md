# 02-25-2021 PSS BST

---

Class: #algo 
 
Week: #week/week-5 
Tags: #algo/BST #algo/sorting #lecture
Related: [[Tree]]

---

- Could have done the nut/bolt problem as a BST, works very similarly to binary search in a tree

## What can you do with a BST?
- Nodes are linked via reference
-> like a linked-list but better
- In any case where you use a BST and recursion you *could* be using a stack instead but ==recursion basically gives us a stack==

**✏ Ex: Give all events between a date range**
- Could hold in a BST: $O(\log n)$
	- The cost is maintaining the sorted items

**Other ideas for data structures: **
- In a list 
	- Items can be added and removed at-will which is expensive to deal with in an indexed list ($O(n)$) but you can use binary search
- In a linked list 
	- Adding and removing is easy but you can't do binary search
- So, use a BST!
	- Dynamic data set which is ordered
	- Add: $O(\log n)$
	- Remove: $O(\log n)$
	- Search: $O(\log n)$

>⭐ BST stuff can still be $O(n)$ - log runtime only comes from halving things so if that doesn't happen in the alg. it could still be $O(n)$

> Adding a size counter to each node with the number of nodes below it can really improve the runtime of some algorithms but there is a small space/time cost of maintaining it

