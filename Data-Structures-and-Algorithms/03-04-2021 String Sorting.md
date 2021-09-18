# 03-04-2021 String Sorting

---

Class: #algo 
 
Week: #week/week-6 
Tags: #algo/sorting  
Related: 

---

# String sorting
- Usually looks from right to left (least significant to most)

## Key-indexed counting
- Can use when sorting small numbers
- Stable sort: duplicates will be right after one another


1. Count the frequency of each key value using the key as an index for an artillery array
	- If the key value is `r`, increment `count[r+1]`
2. Use this count array to compute the starting index position in the sorted array for each item associated with that key, turning `count` into an index table
	- Sum up the counts of smaller values
3. Go through the original array and for each value you come across use the new index table to put the items where they should be in another auxiliary array of the same length as the first
	- As you add, increment the values in count for that key so you do not overwrite the first value you put in
	- Sorts in one pass
4. Copy back into the original array

### Runtime
$O(n)$ Several passes through but it's a series and not nested

## LSD Radix Sort
- Least significant digit first
- Strings are same length
- Replies upon key-indexed counting: to sort strings of $w$ characters, do $w$ key-indexed counting sorts, one for each character position from right to left

### Runtime: 
$O(n)$ always makes $w$ passes through the data

## MSD Radix Sort 
- Most significant digit first
- Strings may be of different lengths
- Recursive
- Partitions the array into subarrays like quicksort except partitions into one subarray for each possible value of the first character (many small subarrays)
	- Must handle these small subarrays well, use insertion sort for small subarrays
- Cost depends on the size of the alphabet
- Slow for subarrays with many equal keys 
- Requires auxiliary and count array

### Runtime
- Depends on the input being random or not but all are around $O(n)$

## Three-way string quicksort
Like [[Quick Sort]]
- Three-way partitioning on the leading character of the keys
	- Less than, equal to, greater than
	- Recursively sort these, ignoring the first character in the middle (all first characters are the partitioning character) subarrays
- Always has three subarrays (fewer than MSD) but requires more movement between them than MSD
	- Handles duplicates well, strings with long similar prefixes, etc. Where MSD runs slowly
- Constant space