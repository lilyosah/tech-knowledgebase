# DP Library Scheduling Example

---

Class: #algo/dynamic-programming 
Week: #week/week-9 
Tags: 
Related:
- [[Dynamic Programming]]

---

## Problem
You have to stack $n$ books on shelves of length $L$
For each book $i$, you are given:
- its height $h_i$
- its thickness $t_i$

The books must be places in the given order 1, ... $n$
Determine which books should go on each shelf given following goals:

<br/>

## Optimization Goal 1: Minimize the Number of Shelves Used
Iterate through the books in order and fill each shelf as much as possible. When full, start another. 
$O(n$)

### [[Greedy Algorithms#Exchange Argument|Exchange Argument]] for Greedy Algorithm
Consider another arrangement of books where $i$ is the first book placed on a different shelf than the greedy algorithm

Because the books **must** be in order, the book must appear on some shelf $s' > s$ where $s'$ is the alternative shelf and $s$ is the shelf used by the greedy algorithm. 

Because it's possible to move book $i$ back to shelf $s$, this cannot decrease the number of shelves used

<br/>

## Optimization Goal 2A: Minimize the total height of the shelves used, assume all books are the same height
You can adjust the height of the shelves to make a perfect fit
This is the same as minimizing the number of shelves #❓ 

<br/>

## Optimization Goal 2B: Minimize the total height of the shelves used, books are NOT the same height
Greedy doesn't work so use [[Dynamic Programming]]

### Recurrence
- First book must go on the first shelf
- Second book could be on previous shelf or a new shelf
- Third could be by itself, with the second, or with the first and second

The $k$th book could be by itself, with $k$ - 1, with $k$ - 2, ... up to the shelf length limit

Let $OPT(i)$ be the cumulative shelf height of books 1 through $i$

Recurrence:
$OPT(i) = _{j \le i}^{min} \{OPT(j) + _{j<k\le i}^{\text{max} h_i} \}$

Shelf containing book $i$ must start with some $j$, we want to minimize the height.

Starting with $i$ = 1, where $OPT(1) = h_1$ iterate through the books and use recurrence to compute $OPT(i)$, saving values as we go.

Runtime is $O(n^2)$ because for each of the $n$  books we have to look at all the options for books that could start at that shelf

