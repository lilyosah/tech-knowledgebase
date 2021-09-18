# Minimum Spanning Tree
#algo/graphs 
#concept
**Related:**
-  [[Graphs]]
-  [[Shortest Path Algorithms]]

---

## Definition
==Minimum Spanning [[Tree]]s:== A subgraph of a weighted, undirected graph that is **spanning** (all vertices are connected) and has **minimum total weight** (sum of the weights of its edges is minimized) ^b35730

This implies **no redundancy:**
- No cycles
- If a cycle has a unique heaviest edge, it is not part of any MST because you could reach the other nodes without using that edge

*For more graph definitions: [[Graphs]]*
## Algorithms to Find MSTs
### Reverse Delete Algorithm
**Algorithm:**
1. Sort edges in order of weight $O(ElogV)$
2. Iterate through the edges $O(E)$
	- Determine if removing the edge disconnects the graph and if it does, do not delete it $O(V+E)$

| Time     | Space  |
| -------- | ------ |
| $O(V^2)$ | $O(1)$ |

We can do better if we think about whether to include or not instead of whether to delete.

### Conditional Edge Inclusion Aglorithms
==Graph cut:== A partition of vertices into two **disjoint** subsets
==Crossing the cut:== Edges where one endpoint is in each group

- A spanning subgraph would include an edge that crosses every cut *(we just need one of these)*
-	For a MST, we need the lightest edge that crosses every cut
- If all edge weights are distinct,
	- For a cut if $e$ is the minimum-weight edge crossing the cut, **every MST of the graph must contain $e$**

#### Prim's Algorithm
**Algorithm:**
1. Start with $X$ = empty subset of edges
2. Initially, $S$ = some arbitrary vertex
3. While $X$ does not span all vertices:
	- Pick lightest edge of all nodes in $S$ ($e = \{u, v\}$ where $e$ is not in $X$)
	- Add $e$ to $X$ and $v$ to $S$

| Time                  | Space      |
| --------------------- | ---------- |
| $O(E \log{E}) / O(E\log{V})$ | $O(V)$ #❓ |

*Because we can use a [[Heap]]/[[Priority Queue]] of edges that we can now reach *

#### Kruskal's Algorithm
**Algorithm:**
1. Sort edges in increasing order of weight
2. For each edge $e$ in that order
	- Include $e$ in MST if adding it does not induce a cycle

| Time                  | Space      |
| --------------------- | ---------- |
| $O(E \log{V})$ | $O(V)$??? #❓ |
*Dominated by sort*

## Verify a MST
- Could compute a MST using an algorithm and then verify that their total weight is the same

Could see if there is a graph that has a better runtime
- If one edge should not be in the tree and another should 
- If you add the edge you need you no longer have a tree because it creates a cycle, so get rid of the most expensive edge in that cycle 

Must verify that T is a spanning tree.
- Traverse the graph and for every node, see if we reach all nodes and ...

Improving:
$O(V)$ time because a tree
- Modify to record the heaviest weight encounters in reaching every other vertex
	- This pre-computes heaviest edges in $O(V^2)$ time