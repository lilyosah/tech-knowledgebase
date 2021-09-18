# Graphs
#algo/graphs 
#concept
**Related:**
-  [[Topological Sort and Strongly Connected Components]] 
-  [[Minimum Spanning Tree]]
-  [[Shortest Path Algorithms]]
-  [[04-15-2021 Graphs PSS]]

---

## Definition
**Basic definitions**
==Graph:== A set of vertices and a collection of edges that each connect a pair of vertices 
- We write $G = (V, E)$, and people usually say a graph has $n$ nodes and $m$ edges
- ==Edges/links:== Connections
	- ==Incident Edges:== Connected by a vertex
- ==Vertices/nodes:== The items
	- ==Degree:== Number of neighbors a vertex has. Number of edges incident
	- ==Sink:== In a directed graph, a node or component which is pointed to but does not point to anything else
==Component:== A portion of a graph 

**Properties of graphs**
==Density:== The number of connections between nodes
==Complete graph:== all nodes are connected (n^2) 
==Connected:== There is a path between every node 
==Strongly Connected:== Every node in this set is reachable from each other
==Disconnected:== Some nodes are not connected
![[Minimum Spanning Tree#^b35730]]

**Types of graphs**
==Undirected Graph:== Edges are bidirectional 
- Edges are unordered pairs of vertices, $m$ is at most $n(n-1)/2$

==Directed graphs:== Edges go in certain directions, edges are ordered pairs of vertices
- Edges are ordered pairs of vertices
	- $m$ is at most $n(n-1)$

==Weighted graphs:== Edges are numbered
==[[Tree]]==: A graph containing one path between any pair of nodes
- Acyclic
- $n-1$ edges

**Traversals**
==Path:== Sequence of edge traversals
- ==Walk:== A path that can repeat nodes
- ==Diameter:== The maximum of all vertices of the shortest path from one vertex to the furthest vertex from it. 

<br/>


## Representing graphs in a data structure
### Adjacency [[Set]] or [[Map]]
>✨ Benefits:
> - Easy to add/remove vertices and edges
> - Easy to use arbitrary objects as keys 


**Unweighted:** [[Map#HashMap|HashMap]]<Vertex, [[Set#HashSet|HashSet]]\<Vertex>> graph
- Maps vertices to sets of neighbors

**Weighted:** [[Map#HashMap|HashMap]]<Vertex, [[Map#HashMap|HashMap]]\<Vertex, Integer>> graph
- Maps vertices to neighbors and their weights

|                                        |              |
| -------------------------------------- | ------------ |
| Space                                  | $\Theta(V+E)$  |
| Adjacent Query                         | $O(\Theta(1))$ |
| Access the attribute of an edge        | $O(\Theta(1))$ |
| Iterate over the neighbors of a vertex | $O(degree(v))$ |


#### Sample Code Snippets
**To query an edge (u, v): O(1)**
`graph.get(u).contains(v)` 
or `graphs.get(u).get(v)`

**To reverse a graph:**
```
reverse = new Map<Node, Set<Node>>
for node in graph:
	reverse.put(node, new Set<Node>)
	
for node in graph:
	for neighbor in graph.get(node)
		reverse.get(neighbor).add(node)
```

<br/>

### Adjacency Matrix 
Indices represent the nodes
📝 If stored as a fixed-length 2D array, difficult to add/remove vertices

|                                 |                                              |
| ------------------------------- | -------------------------------------------- |
| Space                           | $\Theta(V+E)$                                |
| Adjacent edge query             | $\Theta(1)$                                  |
| Access the attribute of an edge | $\Theta(1)$                                  |
| Iterate over neighbors          | $\Theta(V)$ (have to go through a whole row) |


<br/>

### Adjacency [[List]]
Nodes point to a [[List#Linked List]] of their neighbors

$\Delta$: Max degree

|                                 |              |
| ------------------------------- | ------------ |
| Space                           | $\Theta(V+E)$  |
| Adjacent Query                  | $O(\Delta(G))$ |
| Access the attribute of an edge | $O(\Delta(G))$ |

<br/>

## Traversal
### Breadth-First Search
Visiting all neighbors before going farther.

**Algorithm:**
- Go to all children first, then go to those childrens children
- Worklist is a [[Queue]]
	0. Add root to queue
	1. Repeatedly: Remove node at front of queue, add to traversal order/ mark as visited
	2. Push adjacent nodes into the worklist queue

#### RT
| Time       | Space  |
| ---------- | ------ |
| $O(V + E)$ | $O(V)$ |

#### Code
```Python
def traverse(g, s, worklist, f):
	parents = [None for v in range(g.num_vertices())]
	
	worklist.add(s)
	parents[s] = s
	
	while not worklist.is.empty():
		v = worklist.remove()
		f(v)
		for u in g.adjacents(v)
			if parents[u] == None:
				parents[u] = v
				worlist.add(u)
	return parents
```

<br/>

### Depth-First Search
Going as deep/far as you can first and then working your way back up to other neighbors. Can be implemented recursively or with a [[Stack]] and [[Queue]]

- Keep track of an "explored set": A data structure to track parts of the graph already explored
	- This prevents us from repeatedly exploring vertices when the graph has cycles
	- Use a [[Set]] or if returning a parents [[Tree]], just use the keys of the tree

#### RT
| Time       | Space          |
| ---------- | -------------- |
| $O(V + E)$ | Depends... #❓ |


#### Code - Recursion
```
DFS(u):
	mark u as explored, add u to R
	for edge (u, v) incident to u
		if v is not marked explored then 
			recursively invoke DFS(v)
```

## Related Algorithms
[[Minimum Spanning Tree]]
[[Shortest Path Algorithms]]