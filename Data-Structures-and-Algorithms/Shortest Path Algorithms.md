# Shortest Path Algorithms
#algo/graphs 
#concept
**Related:**
-  [[Graphs]]
-  [[Minimum Spanning Tree]]

---

## Problem
Finding the shortest (least-cost in the case of weighted graphs) path between any two nodes
- Chosen from the perspective of source node, not globally like in [[Minimum Spanning Tree]]


## Dijkstra's Algorithm
*Pronounced "diestra"*
> ❗ Be careful if there are negative edges

- The cheapest edge away from a node to a direct neighbor is the shortest path to the adjacent node, **unless** there are negative values in the graph because then another edge which is more expensive 
- Keep track of a known region where you know the shortest path to each node within in, and the cheapest single edge extension from a path in this region is the shortest path to the vertex

**Algorithm:**
1. Begin with $R=\{s\}$ and an empty [[Priority Queue]]
2. Insert all edges out of $R$ into PQ with priority = weight
3. Until we have shortest paths to all nodes (or the destination)
	- Extract smallest entry from PQ
	- Add the node reached, $v$, to $R$
	- Insert all edges out of $v$ into PQ with priority = the cost of the total paths to get to them

📝 It's basically [[Minimum Spanning Tree#Prim's Algorithm]] with a different PQ

| Time           | Space       |
| -------------- | ----------- |
| $O(E \log{V})$ | $O(V?)$ #❓ |

<br/>

### Negative Edges
Negative edges in the graph as they can make a longer path have a smaller value than a path which is shorter.
- Adding numbers to them does not work because this can change the overall balance of the paths
	- Ex: if you had a path that was 3 nodes and another path that had 2 nodes, adding 1 to each of the 3 would change that path more than the one with 2 nodes 

## Bellman-Ford's Algorithm
#📌 Need to re-watch this honestly or look it up because the video is exhausting
Like Dijkstra's but you update all paths for all edges every time, because greedy doesn't work in the case of negative edges
Also works with negative cycles because I guess it knows when it should be able to stop and if it's stuck in a cycle it will be able to detect that 

- Each Iteration we update all vertices
	- Each update involved looking at all incoming edges and calculating the minimum path cost over all those incoming edges
	- Total iteration time is $O(|E|)$
- Need O(|V|) iterations so the overall runtime is $O(|V||E|)$

Space: Distance results of previous iteration when performing updates in the current iteration so need an array of size $O(|V|)$