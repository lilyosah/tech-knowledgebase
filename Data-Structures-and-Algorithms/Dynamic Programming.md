# Dynamic Programming
%%
#algo/dynamic-programming 
#concept
%%
**Related:**
- [[03-25-2021 DP and Greedy Road Trip PSS]]
- [[04-01-2021 DP Sentence Building PSS]]

**Examples:** ^821f15
- [[DP Fibonacci Example]]
- [[DP and Greedy Interval Scheduling Example]]
- [[DP Library Scheduling Example]]
- [[DP Work Plan Problem Example]]
- [[DP Optimal BST Search Example]]
- [[DP Longest Common Substring Example]]
- [[Dynamic Programming Practice Problems From Text]]

---

## Definitions
> ✨ "A smart way to brute force"

You're basically going through every combination and usually taking the best of a few versions of a subproblem that you can **save work from** to reduce calculations. 

==Memoization:== Saving the computed values of subproblems you will likely encounter again in different recursive stacks to avoid doing redundant work. Usually use a [[Map]], used in top down approaches ^634023

==DP Table:== Saving the computed values of subproblems to be used in solving larger subproblems. Usually use a 2D array, used in bottom up approaches ^c79074
- 📝 Note that *usually* the best approach is the iterative version using a DP table (because the space of the recursion stack), but this is case-dependent and they may have different runtimes.

<br/>

**Applications:**
- Problems where you need to evaluate a choice relative to others and something down the line could make the current choice a good or bad one
	- 📝 If you can make choices as you go, use a [[Greedy Algorithms|greedy algorithm]]
	- Many examples are in [[Dynamic Programming#^821f15|examples list]] above

<br/>

## Process
### 0. Develop a recurrence
1. State the idea in words first: Think about it in terms of what you are doing at each step. 
	Ex: At each step I am either adding this value or not.
2. Identify base cases
### 1. Identify dependence on subproblems
Usually you might be doing something like calling max() on two calls to the recursive program where you are either doing the thing at that step or not.
### 2. Identify what information needs to be saved (memoization) and the order of evaluation
Usually this is done with something like a [[Map]], so store the result of max in a dictionary and before you do recursive calls check if the ideal answer to this subproblem is already in the map.
### 3. Convert recurrence to iteration
At this step you will not need memoization because you can take a bottom-up approach so use something like a [[Dynamic Programming#^c79074|DP table]] instead and think about a bottom-up approach where you complete smaller subproblems before the larger ones, and then solve the original problem using the table.

## Runtime
$\text{number of subproblems} * \text{work per subproblem}$

Generally the runtime is every possible combination (if work is constant) because it's a smart brute force. 

### Space
- Think of as filling out a table with different info. 

## Tips

![[Pasted image 20210414180230.png]]