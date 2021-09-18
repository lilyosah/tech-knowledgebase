# Greedy Purchase Schedule Example

---

Class: #algo 
Week: #week/week-9 
Tags: #lecture 
Related:
- [[Greedy Algorithms]]

---

## Problem
You need to buy $n$ items, and you can buy one per month. Each item costs $100 right now.

Prices of each item $i$ increases at a rate of $r_i \ge 1$ per month. After $k$ months, the price will be $100 * r_i^k$

Determine the optimal order to buy the $i$ items to minimize the purchase cost. 

### Greedy Attempt
Want to put in some order

Ex: $r_1 = 1$, $r_2 = 2$, $r_3 = 3$, $r_4 = 4$ 

- if we purchase in increasing order of rate: $100(1^0 + 2^1 + 3^2 + 4^3) = 2800$
- if we purchase in decreasing order: $100(4^0 + 3^1 + 2^2 + 1^3) = 900$

#### Exchange Argument
If we use a solution that is not decreasing rate, at least one month $m$ the purchases are made out of order => $r_m < r_{m+1}$

Swap these purchases in the other solution 
- The contribution in all months other than $m$ and $m+1$ is unchanged
- For these two months:
	- Originally: cost was $100*(r_m^m + r_{m+1}^{m+1})$
	- After the swap: cost is $100*(r_m^{m+1} + r_{m+1}^{m})$
- If the first one is smaller, greedy is better #❓
- $100*(r_m^{m+1} + r_{m+1}^{m}) < 100*(r_m^m + r_{m+1}^{m+1})$
	- Using algebra, this is true



