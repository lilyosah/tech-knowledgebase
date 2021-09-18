# DP Longest Common Substring Example

---

Class: #algo/dynamic-programming 
Week: #week/week-10
Tags: 
Related:
- [[Dynamic Programming]]

---

## Problem
Given two strings, $X = x_1 x_1 ... x_n$ and $Y = y_1 y_2 ... y_m$

Find the longest common contiguous substring (LCS) of these strings

<br/>

## Brute Force
$O(n^2)$ substrings of $X$: for each substring, linear search in $Y$ would tell us if it is present
Total time: $O(n^2*m)$

<br/>

## [[Dynamic Programming]] Recurrence Idea
Either:
- The first letters **match**
	- If LCS **includes both of those positions**
		- Longest common prefix of $X$ and $Y$
	- If LCS **does not include both positions**
		- Left with the two cases below
- The first letters **don't match** (or first letters match but LCS does not include both positions)
	- LCS will not match both $X[0]$ and $Y[0]$, but could match one. 
	- Remaining cases: *cutting off the first letter of the one where it matched*
		- $X[1:]$ and $Y[:]$
		- $X[:]$ and $Y[1:]$
		- LCS of these two cases will be the answer

#📌 *should type this out*
![[Pasted image 20210330212836.png]]
*First part of the recurrence is still complicated*

Asking about the first letters didn't simplify the problem very much 

<br/>

## Recurrence Idea 2
For any starting position of a potential substring in position $i$ in $X$ and $j$ in $Y$:
either
- $X[i] \ne Y[j]$ so substring is len 0
- $X[i] = Y[j]$ so substring is of length 1 + the LCS starting at i + 1 and j + 1 

Now the only work is looking at two characters and in the case of a match looking at a subproblem

#📌 *should type this out*
![[Pasted image 20210330213421.png]]

