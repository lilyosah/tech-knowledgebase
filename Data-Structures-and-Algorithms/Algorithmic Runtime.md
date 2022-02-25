# 01-28-2021 Intro. to Algorithmic Runtime
---
Class: #algo 

Week: #week/week-1 
Tags: 
#algo/runtime #lecture #algo/logarithms

---

 <br/>

## Runtime rules of thumb:
1. **$n^a$ dominates $n^b$ if $a > b$**
    **✏ Ex:** $n^2$ dominates $n$.

2. **Drop constants**
    **✏ Ex:** $14n^2$ becomes $n^2$
    	-> but not $n$'s! $n\log n$ is exactly that, *NOT* $\log n$.
		
3. **Exponential dominates polynomial**
    **✏ Ex:** $3^n$ dominates $n^5$ (it even dominates $2^n$)
	
4. **Polynomial dominates logarithm**
    **✏ Ex:** $n$ dominates $(\log n)^3$
    **✏ Ex:** $n^2$  dominates $n\log n$
	
5. **Don't confuse nested loops ($O(n^2)$) with a series of separate loops ($O(n)$)**
	 **✏ Ex:**
	```Python
	for i in n:
		for j in n[i]:
			#do something
	```
	vs.
	```Python
	for i in n:
		#do something
	for j in n:
		#do something
	```
	
>⭐**Geometric/Arithmetic Series**: 
>If a pattern ends up looking something like: 
>$n + n/2 + n/4 ... 1$
>this is a geometric series and **the first term ($n$ in this case) dominates** because the decay is very significant and it will never add up to $n$
>Similarly, if the pattern is similar to: $n + n-1 + n-2 + n-3 ... 0$ 
>this is an arithmetic series and **the first term ($n$) dominates** because $(n - 1) + (n - 2) ... 0 \lt 2n$, which yields $O(n)$
>This can also happen for work done in recursive levels as explained in [[02-11-2021 Divide and Conquer#^64b43d]]

^cfaac9

---

 <br/>

## How to Evaluate Algorithms
Consider **correctness** & **efficiency**

Correctness:
- have comprehensive test cases

Efficiency in terms of:
- time complexity
- space complexity

 <br/>

### Evaluating Efficiency
$T(n)$: Runtime of an algorithm when the input size is $n$


 <br/>

#### Big-O notation
 : a way to overestimate these trends by specifying an upper bound (worst case)

- $T(n) = O(f(n))$ if for some constant $c$ such that for all $n \ge n_0, T(n) \le c *f(n)$
>$f(n)$ is the **upper bound** of $T(n)$
>$f(n)$ **captures the trend** of $T(n)$

![runtime2|400](runtime2.png)

 <br/>

#### Big Omega notation
: specify a lower bound for a algorithm (best case)

- $T(n) = \varOmega(n)$: $\varOmega(n)$ is $T(n)$'s **lower bound**

![runtime1|400](runtime1.png)

 <br/>

#### Big Theta notation
: specify a tight bound

- $T(n) = \varTheta(f(n))$ if $T(n) = O(f(n))$ and $T(n) = \varOmega(f(n))$
    - This is the only runtime trend possible

> 📝 Technically $T(n) \in O(f(n))$ but people usually just write $T(n) = O(f(n))$
---

 <br/>

### Comparing Efficiency
#### ✏ Ex 1: Using ratios

**Algorithm 1:** $T_1(c) = 10n$

**Algorithm 2:** $T_2(c) = n^2$

 <br/>

We can compare these algorithms using a ratio:

$\dfrac{T_1(n)}{T_2(n)} = \dfrac{10n}{n^2} = \dfrac{10}{n}$ This approaches zero as $n \to ∞$

 <br/>

##### Analysis: 
This is not the same order of magnitude (ratio would == 0). $T_2$ grows much faster, thus **$T_2$ serves as an upper bound** or $T_1(n) = O(T_2(n))$

 <br/>

#### ✏ Ex 2:
**Algorithm 1:** $n\log n + 3n$
-> $n\log n$ is dominant

**Algorithm 2:** $5n + \log n$
-> $5n$ is dominant

 <br/>

##### Analysis: 
$n\log n > n$ because $\log n > 1$ for $n > b$ where $b$ is the log base

-> $T_2$ performs better so $T_2(n) = O(T_1(n))$

---

 <br/>

## Logarithms introduction
Logarithms occur in runtime when an algorithm repeatedly reduced the problem size by a constant factor

>**📝 What is the base?** Usually computer scientists work in base 2 but it doesn't matter in this case because changing the base of a logarithm is the same as multiplying by a constant (which makes no difference in asymptotic notation)
 

**How many times can this repeated division be done?**

$\dfrac{n}{2^x} = 1$

*Multiply by $2^x$*

$n = 2^x$

*Take log of both sides*

$\log_2 n = x$ 

 <br/>

###### Change of base formula:
To write a base-b logarithm as a base-c logarithm:

$\log_b n = \dfrac{\log_c n}{\log_c b} \implies \log_b n = \varTheta(\log_c n)$ 
for any constant $c$, so usually the base is omitted

 <br/>

### ✏ Ex: Using change of base formula 

To make sense of 

$T(n) = 5^(\log_3 n)$,

*Use change of base formula*

$5^{\log_3 n} = 5^{\dfrac{\log_5 n}{\log_5 3}}$

$= {(5^{\log_5 n})}^{\dfrac{1}{\log_5 3}}$



$= n^{\dfrac{1}{\log_5 3}}$ which is a polynomial

*If you wanted you could change it back to its original base to get the general rule*

$b^{log_c n} = n^{log_c b}$