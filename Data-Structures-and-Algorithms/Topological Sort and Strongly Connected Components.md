# Topological Sort and Strongly Connected Components
#📥 
#topic
#concept
**Related:**
-  [[Graphs]]

---

### Topological sort
Imagine a directed graph which maps start and end times.
If for each vertex you mark the entrance and exit "time", the largest will have the largest exit time, everything after it in precedence will have a smaller exit time

- Mark entrance time as when you get to it, exit time as when you finish with all of it's children and have to backtrack to it 

Sorting from an adjacency map:
Find a node with no incoming edges, add to beginning, delete the outgoing edges, and repeat
OR 
Find a node with no outgoing edges, delete incoming edges, repeat
- Having a reverse graph helps

Traversal is $O(n)$

==Directed Acyclic Graph (DAG):==
==Strongly connected:== Nodes within a strongly connected group are all reachable from each other
==Strongly Connected Component (SCC):== A sub-graph of vertices that are mutually reachable
- ==Source components:== Cannot be reached from elsewhere in the graph
- ==Sink components:== Cannot reach anything else

You can sort the whole graph by components
Topologically sorting components:

SCC Algorithm and Analysis:
1. Reverse G to get GR
2. Run complete DFS on GR 
3. In order of decreasing finish time:
	1. select vertex v with largest finish time
	2. run DFS from v in G to get the component containing v
	3. delete that component

Each step takes $O(n)$