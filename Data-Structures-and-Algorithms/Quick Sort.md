# Quick Sort
#algo/sorting 
#concept
**Related:**
-  [[Sorting Algorithms]]

---

## Process
: Apply partitioning and [[02-11-2021 Divide and Conquer]] to sorting

- Divide list into a smaller "half" and bigger "half" using a pivot
- Repeat this process recursively, choosing a partition within each of the halves and sorting around it
- Combine trivially, bc smaller and bigger sorted halves together to form the whole sorted list

*pick an item in the list to split on, bigger than that item and smaller*
*classic implementation is element on the right, 5*

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 9   | 4   | 8   | 1   | 3   | 7   | 6   | 2   | 5   |

*smaller <5*
*recursively sort*

 |     |     |     |     |
 | --- | --- | --- | --- |
 | 2   | 4   | 3   | 1    |

*bigger >5*
*recursively sort*

|     |     |     |     |
| --- | --- | --- | --- |
| 8   | 7   | 6   | 9    |

*Split item is in the middle* 

|     |
| --- |
| 5   |

Sorted items get put around split item

 <br/>

### Partitioning
- Want smaller on left, bigger on right
- work from both sides, swap left items bigger than five with items bigger than five on the right
- Swap pivot to the beginning of the larger section (bigger than the pivot)

| 🔴 > 5❕ |     |     |     |     |     |     | 🔵 < 5❕ | ⭐  |
| --------- | --- | --- | --- | --- | --- | --- | -------- | --- |
| 9         | 4   | 8   | 1   | 3   | 7   | 6   | 2        | 5   |


| ✔   | 🔴 < 5 |     |     |     |     | 🔵 > 5 | ✔   | ⭐  |
| --- | ------ | --- | --- | --- | --- | ------ | --- | --- |
| 2   | 4      | 8   | 1   | 3   | 7   | 6      | 9   | 5   |

| ✔   | ✔   | 🔴 > 5❕ |     |     | 🔵 > 5 | ✔   | ✔   | ⭐  |
| --- | --- | -------- | --- | --- | ------ | --- | --- | --- |
| 2   | 4   | 8        | 1   | 3   | 7      | 6   | 9   | 5   |


| ✔   | ✔   | 🔴 > 5❕ |     | 🔵 < 5❕ | ✔   | ✔   | ✔   | ⭐  |
| --- | --- | -------- | --- | -------- | --- | --- | --- | --- |
| 2   | 4   | 8        | 1   | 3        | 7   | 6   | 9   | 5   |

| ✔   | ✔   | ✔   | 🔴🔵 | ✔   | ✔   | ✔   | ✔   | ⭐  |
| --- | --- | --- | ---- | --- | --- | --- | --- | --- |
| 2   | 4   | 3   | 1    | 8   | 7   | 6   | 9   | 5   |

*swap 5 and 8*

| ✔   | ✔   | ✔   | ✔   | ⭐  | ✔   | ✔   | ✔   | ✔   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2   | 4   | 3   | 1   | 5   | 7   | 6   | 9   | 8   |

Recursively sort both halves using the same process around new pivots in each half

## RT

| Time                                         | Space  |
| -------------------------------------------- | ------ |
| Worst case $O(n)$, average case $O(n\log n)$ | $O(1)$ |

<br/>

## RT Analysis
- Partitioning is $\varTheta(n)$
- ==IF the pivot element is the median==, to sort the two halves recursively is $T(n) = 2T(n/2) + O(n) = O(n\log n)$
-> But if the pivot is not the median you shouldn't always do recursion

In worst case, in naive quick sort the pivot is the minimum or maximum of the list
- pivot would give 2 lists of 0 and n-1
- Recursion looks like $T(n) = T(n-1) + O(n) = O(n^2)$
	- This is no better than a linear sort

So, in worst case $O(n)$, but in average case $O(n\log n)$

However, space is $O(1)$ as everything is sorted in-place

---

<br/>

## Median-of-three Quicksort
: look at three positions (e.g. first, middle, last) and pick the middle of the three
- swap this pivot with the item at the last position
- has surprisingly good performance

 <br/>

### Average-case Analysis
Same as picking a random pivot value
If the pivot is in the middle 50% percentile (between 25th and 75th percentile), we'd get
$T(n) = T((3/4)n) + T(n/4) + O(n) = O(n\log n)$
The chance of it being in the 50% is 1/2