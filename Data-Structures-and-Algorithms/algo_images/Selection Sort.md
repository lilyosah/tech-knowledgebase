# Selection Sort
#algo/sorting 
#concept
**Related:**
-  [[Sorting Algorithms]]

---

## Process
: repeatedly find the minimum item and swap with the item in the front of the sorted section
m : min
✔ : already sorted

**✏ Ex:** 
 
|     |     | m   |     |     |     |
| --- | --- | --- | --- | --- | --- |
| 9   | 3   | 1   | 6   | 8   | 5   |
 
| ✔   | ✔   |     |     |     | m   |
| --- | --- | --- | --- | --- | --- |
| 1   | 3   | 9   | 6   | 8   | 5   |
 
| ✔   | ✔   | ✔   | ✔   | ✔   | ✔   |
| --- | --- | --- | --- | --- | --- |
| 1   | 3   | 5   | 6   | 8   | 9   |

<br/>

## Pseudocode
- Two for loops: one to go through each index and one to find the minimum

<br/>

## RT

| Time             | Space  |
| ---------------- | ------ |
| $\varTheta(n^2)$ | $O(1)$ |

<br/>

## RT Analysis
To find the minimum: takes time in relation to remaining unsorted portion of list

1st pass | 2nd | 3rd |4th | ...
-- | -- | -- | -- | --
n | n-1 | n-2 | n-3 | ...

- Arithmetic series from $1$ - $n$ items so  $n$ dominates (See [[01-28-2021 Intro. to Algorithmic Runtime#^cfaac9]])
- ~$\frac{n}{2}$ compares and $n$ exchanges

Final runtime is $\varTheta(n^2)$ because $n * ~n$