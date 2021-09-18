# Insertion Sort
%%
#algo/sorting  
#concept
%%
**Related:**
-  [[Sorting Algorithms]]

---

## Process
 
: Place each successive item in the correct position relative to the ones already examined

 | ✔   |     |     |     |     |     |
 | --- | --- | --- | --- | --- | --- |
 | 9   | 3   | 6   | 1   | 8   | 5   |

 | ✔   | 3 < 9 |     |     |     |     |
 | --- | ----- | --- | --- | --- | --- |
 | 9   | 3     | 6   | 1   | 8   | 5   |

 | ✔   | ✔   | 6 < 9, 6 > 3 |     |     |     |
 | --- | --- | ------------ | --- | --- | --- |
 | 3   | 9   | 6            | 1   | 8   | 5   |

 | ✔   | ✔   | ✔   | 1 < 9, 1 < 6, 1 < 3 |     |     |
 | --- | --- | --- | ------------------- | --- | --- |
 | 3   | 6   | 9   | 1                   | 8   | 5   |

... Etc. 

 <br/>

## Pseudocode
- For loop to go through $n$
	- Nested while loop to repeatedly swap smaller items with bigger items within sorted section

 <br/>

## RT

| Time                     | Space  |
| ------------------------ | ------ |
| $O(n^2)$, $\varOmega(n)$ | $O(1)$ |

<br/>

## RT Analysis
- At every step you make 1 unit of improvement
- At worst, at each step must look through all of sorted section, (1 sorted items, 2 sorted items, 3 ... $n$)
-> Arithmetic series so $n$, that times the first $n$ is $O(n^2)$
- Best case it's already sorted so you never need to swap (never go through the while loop)

