# Greedy Algorithms
#algo/dynamic-programming 
#concept
**Related:**
-  [[03-25-2021 DP and Greedy Road Trip PSS]]
**Examples:**
-  [[Greedy Purchase Schedule Example]]
-  [[DP and Greedy Interval Scheduling Example#Greedy Algorithm Idea]]
- [[DP and Greedy Interval Scheduling Example]]

---

## Definition
Algorithms where it is appropriate and efficient to make a choice as soon as it is presented and stick with it - information further down the line will not affect the impact of this decision

**Applications:**
- When you don't need to consider every possible combination of options
- You can pick things as you go
- Picking one thing will not prevent you from picking another farther down the line

<br/>

## Exchange Argument 
How to justify using a greedy algorithm.

Process:
1. Consider a different solution than the one produced by the greedy algorithm
2. Show that changing the other solution to that of the greedy algorithms will result in no loss (or show that greedy it is an improvement)

To do this, it may help to put choices in some natural order and consider the first difference between the two.

Usually this can be stated as "If the greedy algorithm is not used, at some point $x$ something will be out of place. This being out of place is no better than the greedy approach because... etc."

Ex: 
- [[Greedy Purchase Schedule Example]]
- [[DP Library Scheduling Example#Optimization Goal 1 Minimize the Number of Shelves Used]]