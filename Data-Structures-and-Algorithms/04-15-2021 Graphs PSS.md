# 04-15-2021 Graphs PSS

---

#📥
Class: #algo/graphs
Week: #week/week-12
Tags: 
Related:
- [[Graphs]]

---

- Graphs are used a lot in cosc
	- Networks, patients to hospitals, etc. 

## Handshake Lemma
Every undirected graph has an even number of vertices of odd degree
: The number of nodes that have an odd number of neighbors is even

Q: Does it matter if the graph is connected?
No

Initial step:
Show the sum of all degrees of all vertices in the graph is twice the number of edges in the graph
- Because each edge creates two neighbors, A is neighbor of B and B is neighbor of A

$Sum(deg(v) = 2 * |E|\*)$
v within G

For this to be true, you couldn't just have one vertex with an odd degree because odd + even is odd, would need to be even + odd + odd to be even

If you have an odd there must be another odd

## Bipartite Graphs
A graph is bipartite if its vertices can be partitioned into two groups s.t. all the edges in the graph have one endpoint in each group
-> Edges go between the two groups, not between nodes within the groups 

Checking neighbors of a node is linear

Algorithm to check if a graph is bipartite:
Breadth-first search through graph, alternatively add the element you're looking at to the first set, then it's children to the other set, if there are ever duplicates then it is not bipartite

Is this correct?
Must produce yes on bipartite graph, no on not
- Yes: ... missed
- No: If it says no then there is a connection between nodes that creates a cycle (odd cycle)
	- This is not bipartite
	- ![[Pasted image 20210415164258.png]]

Runtime:
$O(V + E)$ (linear) Visiting every neighbor of each node
Space:
$O(V)$

## Semi-Connected Graphs
A directed graph is semi-connected if for every pair of vertices u and v, there is a path from u to v or from v to u or both 
This is different from the previous def. because you can't necessarily get from one node to every other node if there are edges in only one direction

More simple version:
Assume it is acyclic 
==Acyclic (a DAG):== no cycles
A DAG is semi-connected iff it has a unique topological ordering 
To get a topological ordering: 
- find a source node, delete it from the graph, and repeat
To determine if a graph has a unique topological ordering:
- if there is more that one source node, it is not
📝 When you care about reachability/paths, use depth-first search

