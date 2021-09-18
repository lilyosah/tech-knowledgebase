# Merge Sort
#algo/sorting 
#concept
**Related:**
-  [[Sorting Algorithms]]

---

## Process 
: Applying [[02-11-2021 Divide and Conquer]] to the problem of sorting
- Divide list into two halves
- Call recursive mergesort function on both halves
- Combine by merging the two sorted lists into one 


 <br/>

### Merging
To merge two sorted lists:
- Keep track of smallest in each list and continually compare those two to each other, put the smallest in the final list and then advance that pointer

| 🔴  |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 1   | 4   | 6   | 9   | 15  | 16  |


| 🔵  |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 2   | 3   | 5   | 7   | 10  | 12  |

| 🔴  |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1   |     |     |     |     |     |     |     |     |     |     |     |

*Compare the next smallest in the list that had the smallest #*

|     | 🔴  |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 1   | 4   | 6   | 9   | 15  | 16  |


| 🔵  |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 2   | 3   | 5   | 7   | 10  | 12  |

|     | 🔵  |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 2   |     |     |     |     |     |     |     |     |     |     |

*same process*

|     | 🔴  |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 1   | 4   | 6   | 9   | 15  | 16  |


|     | 🔵  |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 2   | 3   | 5   | 7   | 10  | 12  |

|     |     | 🔵  |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 2   | 3   |     |     |     |     |     |     |     |     |     |

*etc.*

 <br/>

## Pseudocode
- Recursive sorting
- Base case is one item
- Call mergesort of the first and second halves of the list
- Then merge those together into a new (more space) or the original array (passing indices of interest)

<br/>

## RT

| Time         | Space  |
| ------------ | ------ |
| $O(n\log n)$ | $O(n)$ | 

<br/>

## RT Analysis
For one call to mergesort:
- Divide: trivial to compute midpoint O(1)
- Recurse: sort both halves recursively
- Combine by merging
	For merging: 
	- For each item in list, $O(1)$ to put item in 
	- Must go through both half lists so $\varTheta(n)$ time and $\varTheta(n)$ space (if using the same array in-place and using an auxillery array)

Recurrence rel.:

$T(n) = O(1) + O(n) + 2T(\frac{n}{2}) = O(n\log n)$


Solving the recurrence for practice:

$$
\begin{align}
T(n) &= 2T(\frac{n}{2}) + O(n) \\
T(n) &\le 2T(\frac{n}{2}) + c*n \\
&\le 2(2T(\frac{n}{4}) + c*(n/2)) + c*n \\
&\le 4T(\frac{n}{4}) + 2c*n \\
&\le 4T(2T(\frac{n}{8}) + c(n/4))+ 2c*n \\
&\le 8T(\frac{n}{8}) + 3c*n
\end{align}
$$

Generalized pattern: $T(n) \le 2^kT(\frac{n}{2^k})+kcn$
At $k = \log2 n$, $T(n) = \log2 n * cn$
Which means
$T(N) = O(n\log n)$

>The disadvantage is that the space used is $O(n)$ (for an auxillery array if you're sorting in place)

## Tree
// Insert picture here