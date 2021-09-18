# DP Fibonacci Example

---

Class: #algo/dynamic-programming 
Week: #week/week-9 
Tags:
Related:
- [[Dynamic Programming]]

---

## Computing Fibonacci Numbers
The sequence: 
- $f_0 = 0$
- $f_1 = 1$
- Each subsequent number is the sum of the previous two


### Recursive Fibonacci
```Python
def fib(n):
	if n == 0: return 0
	if n == 1: return 1
	return fib(n-2) + fib(n-1)

```

Computing the $n$th number requires competing two previous numbers:
- $T(n) = T(n-1) + T(n-1) + O(1)$
	- ❗ Subtracting one every call two times is very bad! [[02-11-2021 Divide and Conquer]]

Runtime is about $O(1.618^n)$

### Memoization to Eliminate Redundant Work
```Python
# This keeps track of the previous numbers you've computed
memo = dict()

def fib(n):
	if n == 0: return 0
	if n == 1: return 1
	
	if n not in memo:
		memo[n] = fib(n-2) + fib(n-1)

	return memo
```

❗ Notice you only ever need to know the previous two numbers so you can convert this to an iterative solution

### Converting to Iterative Solution

```Python
def fib(n):
	if n == 0: return 0
	if n == 1: return 1
	
	f1 = 0
	f2 = 1
	
	while n > 1:
		nxt = f1 + f2
		f1 = f2
		f2 = nxt
		n-= 1

	return f2
```