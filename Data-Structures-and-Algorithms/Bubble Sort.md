# Bubble Sort
%%
#algo/sorting 
#concept
%%
**Related:**
-  [[Sorting Algorithms]]

---

## Process
: Swap adjacent out-of-order items

*Pass 1:*
 
 | ➡   | ⬅   |     |     |     |     |
 | --- | --- | --- | --- | --- | --- |
 | 9   | 3   | 6   | 1   | 8   | 5   |

 |     | ➡   | ⬅   |     |     |     |
 | --- | --- | --- | --- | --- | --- |
 | 3   | 9   | 6   | 1   | 8   | 5   |


 |     |     | ➡   | ⬅   |     |     |
 | --- | --- | --- | --- | --- | --- |
 | 3   | 6   | 9   | 1   | 8   | 5   |

 |     |     |     | ➡   | ⬅   |     |
 | --- | --- | --- | --- | --- | --- |
 | 3   | 6   | 1   | 9   | 8   | 5   |


 |     |     |     |     | ➡   | ⬅   |
 | --- | --- | --- | --- | --- | --- |
 | 3   | 6   | 1   | 8   | 9   | 5   |


 |     |     |     |     |     |     |
 | --- | --- | --- | --- | --- | --- |
 | 3   | 6   | 1   | 8   | 5   | 9   |

*Pass 2:*

 |     | ➡   | ⬅   |     |     |     |
 | --- | --- | --- | --- | --- | --- |
 | 3   | 6   | 1   | 8   | 5   | 9   |

 |     |     |     | ➡   | ⬅   |     |
 | --- | --- | --- | --- | --- | --- |
 | 3   | 1   | 6   | 8   | 5   | 9   |

 |     |     |     |     |     |     |
 | --- | --- | --- | --- | --- | --- |
 | 3   | 1   | 6   | 5   | 8   | 9   |

... Etc.

Notice: 

| 1st pass                                      | 2nd pass                         | 3rd pass                     |
| --------------------------------------------- | -------------------------------- | ---------------------------- |
| Biggest 1 item is sorted correctly at the end | 2 end items are sorted correctly | 3 end items sorted correctly |

-> Every pass you make one unit of progress

 <br/>

## Pseudocode
- Two for loops: one to go through, one to only look at up to $n$-`i` items (because after that point you know it's all sorted)
	- Nested for loop that goes up to `i` to swap if out-of-order
	- To improve runtime: maintain a count variable and conditional break every loop so that if you didn't swap anything that round exit both loops

 <br/>

## RT

| Time                     | Space  |
| ------------------------ | ------ |
| $O(n^2)$, $\varOmega(n)$ | $O(1)$ |

<br/>

## RT Analysis
Again, you have

| 1st pass | 2nd | 3rd | 4th | ... |
| -------- | --- | --- | --- | --- |
| n        | n-1 | n-2 | n-3 | ... |

items to iterate through and check which sums to $O(n^2)$, but notice lower bound is not $n^2$ because you have conditions to end early if it's already sorted