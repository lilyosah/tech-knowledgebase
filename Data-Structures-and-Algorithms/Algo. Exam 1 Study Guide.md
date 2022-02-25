# Algo. Exam 1 Study Guide

---

Class: #algo 
Week: #week/week-7
Tags: #study-guide
Related:
Format: 
- Problem solving questions like labs
- More conceptual, can explain in prose of pseudocode or both

---

### How to study:
- Review notes
- Review labs
- Review PLTL problems
- Review problem solving sessions?

--- 

## Week 2 - Complexity
- [x] Concepts [[Algorithmic Runtime]] [[Disjoint Sets]] 
	- ❕ Tight bound requires showing the upper and lower bounds
- [x] [Lab](https://www.notion.so/Topic-1-Lab-Questions-and-Solutions-6df4fa6fc95347d8b044ee82b85bcc35)
	- Array Sums:
		1. O(n^3)
		2. Instead of adding up every entry from i-j keep track of a sum and just add the next element every time
	- Jar Drop:
		1. BST with jars O(log n)
		2. Linearly work your way up from the bottom O(n)
		3. Drop the first half way, then depending on whether it breaks or not work your way up linearly from the middle or bottom O(n/2) = O(n)
- [ ] [PLTL](https://www.notion.so/PLTL-1-Problems-and-Solutions-fed82da3ebba46188b7c506d8fc344b6)
	- 

---

 <br/>

## Week 3 - Search 
- [x] Concepts [[Data Structures]] [[Sorting Algorithms]]
- [x] [Lab](https://www.notion.so/Topic-2-Lab-Questions-and-Solutions-d3e15c8d24574b279dc784fc811e859b)
	- Search in a sorted, rotated array
		- Search: Do a modified binary search
			- Get middle element
				- If t > mid, take rightmost mid
					- If rmid < mid, 
						- Take leftmost mid, repeat process
				- If t < mid, take leftmost mid
					- If lmid > mid, 
						- Take rightmost mid, repeat process
- [ ] [PLTL](https://www.notion.so/PLTL-2-Problems-and-Solutions-f47fdb8a7e384a00a941007f767339d0)

---

 <br/>

## Week 4 - Recursion and Divide and Conquer 
- [x] Concepts  [[02-11-2021 Divide and Conquer]]
- [x] [Lab](https://www.notion.so/Topic-3-Lab-Questions-and-Solutions-d274e808228046b9a7891bba3ab6c0f1)
	1. Unimodal Array
		- Binary search, 
			- If mid >= lmid
				- Search on right half
			- Else
				- Search on left half   
- [ ] [PLTL](https://www.notion.so/PLTL-3-Problems-and-Solutions-58b9b79bc1914cba8584ce6471685100)

---

 <br/>

## Week 5 - Sorting and Selection 
- [x] Concepts [[Sorting Algorithms]]
- [x] [Lab](https://www.notion.so/Topic-4-Lab-Questions-and-Solutions-805f04cec055441985945b83bdf0edf7)
- [ ] [PLTL](https://www.notion.so/PLTL-4-Problems-and-Solutions-d39bf02b453540618ffd548b8299a683)

---

 <br/>

##  Week 6 - BST
- [x] Concepts [[Tree]] [[02-25-2021 PSS Binary Search Trees]]
	- Recursion is only required if you must take multiple branches though a tree, otherwise you can just loop through
- [x] [Lab](https://www.notion.so/Topic-5-Lab-Questions-and-Solutions-a73e986664b24d62a496a771f5833863)
- [ ] [PLTL](https://www.notion.so/PLTL-5-Problems-and-Solutions-7ca57e0a6d914d0891549588d9b373c8)

---

 <br/>

## Week 7 - String Sorting and Selection
- [x] Concepts [[Trie]] [[03-04-2021 PSS Tries]]
- [ ] Lab
- [ ] PLTL
