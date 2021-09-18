# Shell Sort
#algo/sorting 
#concept
**Related:**
-  [[Sorting Algorithms]]

---

: Uses [[Insertion sort]] interleaving sublists
- Able to use large jumps within the list 
- At some point you'll have to use a regular insertion sort to get the final version

 | 🔴  | 🟡  | 🔵  | 🔴  | 🟡  | 🔵  |
 | --- | --- | --- | --- | --- | --- |
 | 9   | 3   | 6   | 1   | 8   | 5   |

*Compare 9:1, 3:8, 6:5 and swap with those pairs*

 | 🔴  | 🟡  | 🔵  | 🔴  | 🟡  | 🔵  |
 | --- | --- | --- | --- | --- | --- |
 | 1   | 3   | 5   | 9   | 8   | 6   |

## RT?