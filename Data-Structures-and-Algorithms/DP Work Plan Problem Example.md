# DP Work Plan Problem Example

---

Class: #algo/dynamic-programming 
Week: #week/week-10 
Tags: 
Related:
- [[Dynamic Programming]]

---

## Problem
- You have $H$ hours to spend on your work
- You have clients $1... n$
- Each client $i$ has given you a project that will take $t_i$ hours to complete and on completion you will earn $r_i$ money

### Goal 1: Return the optimal set of clients' projects to complete maximizing revenue
- [[Greedy Algorithms|Greedy]] doesn't work: if you just pick the projects that pay the most per time spent on it, so use [[Dynamic Programming]]

Ex: $H = 8$

| t   | r   |
| --- | --- |
| 5   | 10  |
| 4   | 7   |
| 4   | 4   |

Project one is worth the most but if you chose it you could only do that one and you'd be better off doing 2 and 3

#### Step 1: Develop a Recurrence
- must consider the possibility of including any project
	- if we include project $i$: gain $r_i$ and have $H-t_i$ hours of work remaining. We'd like to fill those optimally, so the subproblems are the same as the current one but with $H-t_i$ hours and all projects except $i$
	- if we don't include $i$: We gain nothing but still have the full $H$ hours to fill so subproblems have the same $H$ and all projects except $i$

**Indication that this is good recursion:** # of projects in the subproblems decreases

##### Recurrence
Let:
$OPT(i, H) =$ the optimal $ to be obtained from projects 1 through i, with H hours to work

$OPT(i, H) = max($
- $r_i + OPT(i - 1, H- t_i)$
- $OPT(i-1, H)$
$)$

The answer is represented by $OPT(n, H)$

We also consider the number of hours.
Two options:
1. For each number of problems $i ... n$ **iterate through $h = 1, 2... H$ and compute and answer for each $OPT(i, H)$**
	- RT: $O(nH)$ pseudo-polynomial. $H$ is a value in the input, not the size of the input. Does not scale with the size of the input
		- $n*H$ subproblems to compute and each takes constant time. 
2. **Use memoized recursion:** This could help if we only need sub-problem answers $OPT(i, H)$ for a few values of $h$ (you know you won't likely run into the same subproblems again or if they are intensive to calculate), or if there are discrete values we need but they aren't integers so iterating through them is hard

**Generally with dynamic programming you use option 1, the iterative approach**

##### Base case
The problem we're considering, $i$, depends on subproblems where we do $i-1$ projects, so one part of the base case is 1 project 

#📌  Don't know that I finished this?

