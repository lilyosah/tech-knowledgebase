# # Title

---

#algo/project
##### Due: 04-26-2021
- [Class Notion page](https://www.notion.so/Data-Structures-and-Algorithms-2dc17465f862455b86e8d1051ee41539)
- [Description](https://www.notion.so/HW9-Interval-Consistency-7436239237b94a2bbbb07470acb6539a)
- [ ] Done
- [ ] Submitted

Related:

--- 


## To-do:

- [x]  Implement graph-building function
- [ ]  Implement cycle checking function
- [ ]  Implement interval assigning function
- [ ]  Go back and use hashset instead of graph object
- [ ]  Turn in

---

## Problem Description:
Given a series of start and end points and whether or not they overlap, return null if this combination is not logically possible and a set of those intervals as `IntervalInfo` objects.

## Ideas:
- How do I represent that they overlap?
- If something ends before and after something it is not valid 

Have set of things that have already been evaluated

Find start time add to current set
find end time, remove
Order by end times

Priority Queue ordered by end time?
If i'm just adding them all and then need it sorted might as well use a list

Add the ones that have not ended yet to a set, remove from the set as they end 

Iterate through the set of intervals
For each:


### Idea 1:
#### Build Graph of Start and End nodes 
Have starting and ending nodes for each interval. Each node points to nodes that come before it
- Each **end** points to its **start
Reverse:
- If A overlaps B: 
	- Ae -> Bs 
	- and
	- Be -> As 
- If A ends before B:
	- Bs -> Ae

%%- If A overlaps B: 
	- Bs -> Ae (B starts before A ends)
	- and
	- As -> Be (A starts before B ends)
- If A ends before B:
	- Ae -> Bs
%%

If there is a cycle then the graph is invalid.

#### Traverse the graph
[[Graphs#Traversal]]

Maybe DFS on REVERSE graph, call on every node not visited. 
Keep track of the highest number assigned. At the end of each depth assign that node to the mx+1
Depth first search, at the end of each 

if child has been assigned an interval number


#### Check for cycles
- Make this not recursive


### Data Structures:
#### Start/end Object
SorE var: True if start, false if end
- Set of nodes it points to/ starts before
- Maybe keep track of its end separately if it is a start

#### Graph object
- Set of nodes

### Algorithm Description:
1. 