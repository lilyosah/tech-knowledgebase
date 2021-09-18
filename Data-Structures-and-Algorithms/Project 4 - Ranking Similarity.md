# 4 Ranking Similarity

---

%% #algo #algo/project %%
##### Due: 02-27-2021 #week/week-5 
- [Class Notion page](https://www.notion.so/Data-Structures-and-Algorithms-2dc17465f862455b86e8d1051ee41539)
- [Description](https://www.notion.so/HW4-Ranking-Similarity-0603fd00e8a949c88d78dc33f26c8f67)
- [x] Done
- [x] Submitted

Related:
[[Sorting Algorithms]]

--- 

## To-do:

- [x]  Figure out algorithm
- [x]  Implement
- [x]  Turn in 

---

## Problem Description:
Input: Two arraylists of a generic type which contain the same items (one in each list with .equal() each other)
Output: a double in the range [0.0, 1.0] which represents the similarity of both lists.

Implement a function which determines the ranking similarity of two lists. 
$\text{ranking similarity} = \frac{\text{number of pairs in the same order}}{(n(n-1))/2}$

A pair is in the same order if for two items in one list that form a pair ($a$ and $b$), $a \lt b$ and in another list with the same items $a \lt b$ then they have the same relative ranking in both lists. Different items may come in-between them in each list. It does NOT mean that two items must be at the same index in both lists

Can be done in $O(n\log n)$ time: at its heart, this is a problem about how the elements are ordered, and so you can take advantage of sorting techniques.

Here are two hints to help you get started:

1.  A modification to mergesort can reveal how many out-of-order pairs there are in a list. While sorting a list, when merging the left and right halves, whenever an element is taken from the right half, it was necessarily out-of-order with respect to the number of elements remaining in the left half.

3.  You can use sorting, but rather than putting the ranked items themselves in sorted order (which isn't possible — we don't know that the items of type `T` are `Comparable`), try defining an order based on the first list and sorting the second list (keeping a count of out-of-order pairs as mentioned in the first hint) with reference to that first list's order.

 <br/>

## Ideas:
### Data Structures:
[[Data Structures]]
Input: Two `ArrayList<T>`
- $O(1)$ get and set methods
- Can't assume anything about T other than it is an object. 
To hold list 1 orders: 
`Hashmap<T, Integer>` with mapping [element: its index]. Takes $O(n)$ to put in but this is less than $O(n \log n)$ so I'll go with this


### Algorithm Description:
- Define an order based on on the first list and sorting the second list with reference to that first list's order, keeping a count of out of place items
	- In mergesort [[Sorting Algorithms]] you are putting two lists into one bigger one by putting the smallest item of two sorted lists into a final list to return  
	- To do this in reference to the first list, when you are merging elements back into the array check if that element pair if out of order in the first list. If it is out of order, increment the number of out of order pairs by the elements in the left half that you haven't added yet and place the correct element in. 

Do a regular mergesort on the second list, except instead of comparing whether A > C in the second list, check whether A > C in the first list. If those two items are out of order in the second list compared to the first, then put them in the sorted position and then increment a counter which will keep track of how many switches there have been. Continue sorting in reference to the first and merging back together. 
 
- Making the comparisons to the first list will take O(n) if it's in an array, maybe I could put it into a different data structure?
- The mergesort should be done in an array (passing indices, probably easier) or linkedlist so that the space is O(n) 

