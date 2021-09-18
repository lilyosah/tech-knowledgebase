# Sorting Algorithms

---

[Slides](https://moodle.colgate.edu/mod/folder/view.php?id=483433) 
[Videos](https://medialibrary.colgate.edu/hapi/v1/ui/permalinks/He3n6PGr)
Tags: #MOC #lecture  #algo/sorting
Related: 
- [[02-18-2021 PSS Selection]]

---

## Elementary Sorting Algorithms
==Comparison sorting:== putting a collection of comparable items in order
- Don't assume that you can do aynthing else with the items (sorting)

### Standard Model
- input and output are both lists
- can get/set item at a position in $O(1)$ time
- occupy a fized length in memory, so inserting/removing an item at a position takes $O(n)$ time

Constant time operations:
- comparison
- swapping two items (knowing their positions)

---

### Algorithms

[[Selection Sort]]

![[Selection Sort#RT]]

[[Bubble Sort]]

![[Bubble Sort#RT]]

 [[Insertion sort]]
 
 ![[Insertion sort#RT]]

[[Shell Sort]]

![[Shell Sort#RT]]

## More Advanced Sorts
In general, the best sorting runtime you can hope to get is $O(n \log n)$

[[Merge Sort]]

![[Merge Sort#RT]]

[[Quick Sort]]

![[Quick Sort#RT]]

[[Heap Sort]]

![[Heap Sort#RT]]
