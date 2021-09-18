# 04-01-2021 DP Sentence Building PSS 

---

Class: #algo/dynamic-programming 
Week: #week/week-10 
Tags: #algo/PSS 
Related:
- [[Dynamic Programming]]

---

- Not every subproblem can fit together in a linear way, or cleanly
- Today's problem seems linear but needs a more sophisticated representation to consider choices
- Built subproblems on "natural leftovers of recursion"

## Problem Description
- Given a lot of words, concatenate them together to form a sentence using the least work possible (concatenation is linear time in Java)
- Array of strings, ordered by how they should appear
- You could just concatenate them all together but that might not be optimal because RT depends on length of string


Ex: lengths 3, 7, 10
1. 3 + 7  = 10 -> 10, 10
	10 + 10 = 20 -> 20
	total: 30
2. 7 + 10 = 17 - > 3, 17
	 3 + 17 = 20 -> 20
	 total: 37

<br/>

## [[Greedy Algorithms|Greedy]] Idea 
Concatenate two smallest that are right next to each other 
- This does not always work because of
- 5, 4, 4, 5 example

<br/>

## [[Dynamic Programming|Dynamic]] Idea
-Min of recursively splitting over every possible point and taking the cost of concatenating both sides
	- **Cost** of minimally concatenating a group of strings are the subproblems

**Subproblems:**
Cost of a certain starting index : ending index 

This is enough of an explanation

```
// 1. explain in words what we calculate
Let C(i, j) = the min cost of concatenating strings i through j

// 2. develop recurrence, how does this relate to subproblems?
Recurrence:
C(i, j) = len(i) + len(i+1)...+len(j)
	min over choice of k, where i <= k <= j:
		C(i, k) + C(k+1, j)
		
// 3. Base cases: These are base cases but still happen "first" because calc begins as you begin to return
// single string
C(i, i) = 0
// two strings
C(i, i+1) = len(i) + len(i+1)

// 4. Evaluate these in increasing size of subsequence
// (base cases are 0 and 1, then 2, then 3, .. m)
// answer we want is C(1, m)
```

### RT
 #❓ *Why are these the case? go back and look at the video*
- Go through every split point (m), for every one of those, another m points?? then another m? For O(m^3)
	
Space: in [[Dynamic Programming]] likely to be space used by the memoization structure
- how many subproblems are there?
	- If there's a pair that you have to go through quadratically, quadratic. 
	- O(m^2)

Cost of concatenating 1 + (2, 3, 4, 5) is n + cost of producing (2, 3, 4, 5)
- This indicates a subproblem
	- Memoization of cost of concatenating a certain collection of words
		- in 1 + (2 3 4 5) -> n + 2 + (3 4 5) and (1 2) (3 4 5), (3 4 5) appears, so having this cost saved would be helpful

#❓ *bottom up vs top-down? which is better when*

