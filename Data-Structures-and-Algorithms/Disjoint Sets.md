# 01-28-2021 Intro. to Disjoint Sets

---

Class: #algo

Week: #week/week-1 
Tags: #lecture 
Related: [[Project 2 - Algorithmic complexity Union-Find]]

---


==Disjoint set:== data structure that shows connections and reachability
- The element → set map is stored in a map/dictionary

**Functions:**

- Union: Join two groups into one
- Find: Given an element within the set, return some identifier which represents the group the element is in

 <br/>

## Function Visualization



![[DJSFunctionVis.png|400]]



Operation | Element | Set/Group
------ | ------ | ---- 
$find(1) → 1$  *alone*| 1 | 1 ✓
$union(1, 3)$   | 2 | 2 
$find(1) == find(3)$ *same output*   | 3 | ~~3~~ 1 ✓
$find(5) ≠ find(1)$   | 4 | 4
$union(5, 6)$   | 5 | ~~5~~ 1
$find(5) → 1$   | 6 | ~~6~~ ~~5~~ 

 <br/>

## Quick Find
- Find: looks up the value (set ID) associated with the element (key) in our map 
	-> $\varTheta(1)$
- Union: Go through the table and for every affected element change the set IDs to the one that it is being unioned with 
	-> $O(n)$

**✏ Ex:** 

| Operation   | Desc.                            |
| ----------- | -------------------------------- |
| union(4, 1) | Must change all parents on union |

![Quick find|300](DJSImplementingQuickFind.png)


 <br/>

## Quick Union
- Union: only changes self-representative elements on union (ones that point to themselves
- Find: will continue searching form child -> parent -> child -> parent until something maps to itself 

**✏ Ex:** 

| Operation   | Desc.                                                     |
| ----------- | --------------------------------------------------------- |
| union(1, 4) | only change where 4 maps to                               |
| find(5)     | continue searching until something maps to itself (1 → 1) |


![DJSQuickUnion1.png|600](DJSQuickUnion1.png)
**✏ Ex:** 

| Operation  | Desc.                                                   |
| ---------- | ------------------------------------------------------- |
| union(2, 5) | only change the representative elements (self-pointers) |
| *within union* find(2)    | -> 1                                                    |
| *within union* find(5)    | -> 4, so union changes 1 and 4, not 2                                                        |


![DJSQuickUnion2.png|350](DJSQuickUnion2.png)
**✏ Ex:** 

| Operation   | Desc. |
| ----------- | ----- |
| union(5, 1) |   Doing all the finds to ultimately change 4 (self-pointing) to 1    |

![Quick Union|400](DJSImplementingQuickUnion.png)

 <br/>


## Path Compression

---

: Instead of elements indirectly pointing to another through chaining, make each element directly point to its parent

Without path compression:

```Python
find(x):
	while map[x] != x:
		x = map[x]
	return x

	# or

	if x = map[x]
		return x
	return find(map[x])
```

With path compression:

```Python
find(x):
	while map[x] != x:
		if x = map[x]
			return x
		top = find(map[x])
		map[x] = top
		return top
```

- You can keep track of the heights of each elements find-chain but I'm not sure why?

```java
union(x, y):
	p1 = find(x)
	p2 = find(y)
	//nearly O(1)
	if p1 == p2: 
		return //same set
	if heights.get(p1) < heights.get(p2):
		map.put(p1, p2)
		heights.put(p2, heights.get(p2) +1)
		// theta(1)
```