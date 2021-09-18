# 03-25-2021 DP and Greedy Road Trip PSS

---

Class: #algo 
Week: #week/week-9
Tags: #algo/PSS
Related: 
- [[Dynamic Programming]]
- [[Greedy Algorithms]]

---

## Greedy Vs. Dynamic Vs. More Exhaustive Approach
## Road Trip
Need to stop at places along the way

You have:
- A list of potential places
- A list of all the costs 

Where should you stay?

Requirements / optimization goal:
- At most, you can go 500 miles in a day 

### Version 1: Min Number of Stops
- Make the minimum number of stops 

#### Idea 1
- For each stop, look at stops < 500 miles, go to the farthest stop

##### Proof
- Choose arbitrary (but valid) other algorithm and prove that **greedy is no worse than the other**
	- Line up places that you should stay in "against each other"
	- Look at the first place that the algorithms are different 
	- The day started the same, but end differently
		- The other stop is closer than the greedy one (other <= greedy, will not be fewer stops)

### Version 2: Cheapest
- Where should you stay to minimize the cost of your stops

#### Idea 1
- For each stop, look at stops < 500 miles, go to cheapest
	- Might not work for because you could go to a closer cheap one that's just out of reach of a bunch of cheap ones
	- You would kind of need to go through all of the options, so use [[Dynamic Programming]]
		- Still need to avoid going $O(2^n)$ ? route

#### Idea 2 Dynamic Programming
- When you do dynamic programming, write it out in words first
- Start by developing a sensible recurrence that allows you to connect subproblems 
- the `c(0), c(1) ... etc.` is saving your previous answers
- The final version is usually iterative, not recursive 

```
C(i, places to stay) = min cost of getting from place i to the finish
	considering "places to stay"
	
(assume places to stay are 1, 2, ..., n
index 0 = start
index n+1 = finish)

// base case / finish line
c(n+1) = 0 

c(0, places to stay) = min(
	1. don't stay at place 1, 
		c(0, "places to stay" - {place 1})
	2. stay at place 1 
		cost(place1) + (c1, "places to stay" - {place 1})
	)
	
// alternate formula

c(i) = minimum cost of a trip starting at location i
		min (
		stay at place i+1
			cost(place i+1) + c(i+1)

		stay at place i+2
			cost(place i+2) + c(i+2)

		stay at place i+3
			cost(place i+3) + c(i+3)

		...
)

// iterative approach
C = new list

C[n+1] = 0
for i in n to 0:
	// do the formula above, it's more of a lookup table where you have the previous answers saved
	for j = i + 1 up to place < 500 miles away:
		evaluate cost_stay(j) + C[j]
		if best is None or best > cost:
			best = cost
		
		C[i] = best

```

The runtime of this is $O(n^2)$, compared to the recursive method without memoization where you go through everything and redo work is $O(2^n)$







