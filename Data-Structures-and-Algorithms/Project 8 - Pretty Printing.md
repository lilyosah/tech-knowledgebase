g# 8 Pretty Printing

---

#algo/project
##### Due: 04-16-2021
- [Class Notion page](https://www.notion.so/Data-Structures-and-Algorithms-2dc17465f862455b86e8d1051ee41539)
- [Description](https://www.notion.so/HW8-Pretty-Printing-1aae33cf61894a6d8046f88d897b9719)
- [ ] Done
- [ ] Submitted

Related:

--- 


## To-do:

- [ ]  Plan algorithm
- [ ]  Implement

---

## Problem Description:
**input:** `int[] lengthsOfWords, int maxLen`
**output:** `list of indicies corresponding to the last word on each line in order of lines`

We are emulating pretty printing by outputting a list of word indices of where line breaks should be given a list of the length of words. 

The characters of each line are given by: `len(all words on line) + num words - 1 (spaces`

==Line slack:== The amount of space between the last word in the line and the right margin.

Line slack of words $i$ - $j$ given by: `maxLen - (len of all words in line + (j - i))` 

You can make a slackFunctor object to store the metric you will measure each line by. 

## Ideas:
### Data Structures:
- 

### Algorithm Description:
pass indices in the list to each func version


At each word, you either add it to the current line or you add it to the next

maybe do something similar to the [[Project 7 - Tile Puzzle]] where you take the one with the current smallest slacks and continue a version where you add the next word onto that line and a version where you add the word to the next line   
- The one with the smallest slack will be the one where the sum of the slackFunctor on each line is the smallest 

Are there subproblems?
Individual lines will be repeated, the whole combination will not be 


Start with array that is middle column
- If you choose one that is not on middle, index j - k-1 on array will be 0s, k is the length at that index 
	- Next iteration will choose from j = k (new k)

for each k value, go through the next row (knew > k)  where j > k

```
min = 20 : [6, 5, 4, 5] // middle diagonal
temp = [6, 5, 4, 5]
for k:
	j = k+1
	nMin = 0
	while j < k:
		num = table[j][k]
		nMin += num
		// if nMin >= min, break innermost while
		temp[k] = num
		j++
		
end if k or j == n-1

for k:
	sum = table[0][k]?
	if k == n-1: break
	for j = k + 1; j <= n-1
	

val at j, k can be added to sum that includes all j, k-1 (not right)
	
	
```

if when you're iterating though you ever go above min, end that iteration early


Go through each word in this line.
On each word, make a break here 

```Java

// compute slacks before loop, put into table (all line combinations of words on a line i through j)
int[][]table = new int[len(lengths)][len(lengths)]

// opt is an array
int [] opt = new int[n];
opt[0] = 0

// Will this not only ever make three splits?
// for every word, try making this the last split and then for each word before this one, also try splitting there. The value at the index of the first (k)(as in earlier in the paragraph, so inner for loop) split in the opt array should be the minimum value of the splits that can be made before it 
// dont see why this should start at 1
for k in range (1,n): // 0 or 1?
	// is this the correct initial value for min? if this is here then should the next for loop start at 2 instead of 1 and mode the check somehow??
	// try splitting on every word that comes before this one
	for j in range(0, k+1): // used to be 1
		// assuming you split here, slack of the second line (after split) + plus slack of the line that comes before 
		candidate = functor(table[j][k])) + opt[j]
		if candidate < min:
			min = candidate
	opt[k] = min
	
return opt[n]
```

- words as all separate are the table values down the center diagonal `[0][0], [1][1]` etc.
- Dict that maps something to the break coords

```
sums[0]=0
// save min and also k values, just worry about min for now
for k in range(n):

	// start off as keeping this word separate
	min = table[k][k]
	
	//not inclusive of k, that would be the min value above
	for j in range(k):
	
		// get smallest 
		try = table[j][k]
		
		if try < min:
			min = try
	sums[k] = min + opt[j-1]
			
	add to breaks?
	
	
```

k = 1
	m = 5 + 0
	j = 0
	t = 3  + 0
	m = 3
k = 2
	m = 4 + 3 = 7
	j = 0
	t = 1 + 0
	j = 1
	t = 6 + 3 = 9
	m = 1
k = 3
	m = 5 + 1 = 6
	j = 0
	t = -4 X
	j = 1 
	t = -2 X
	j = 2
	t = 1 + 1
	m = 2

sums (should map to breaks eventually) =

 | 0   | 1   | 2   | 3   |
 | --- | --- | --- | --- |
 | 0   | 3   | 1   | 2   |

Iterate through this in o^2? pull the min where the things dont overlap 

breaks (j, k)

|     | 3    | 1    | 2   |
| --- | ---- | ---- | ---- |
|     | 0, 1 | 0, 2 | 2, 3 |


```
for i in sums:
		


```

| 0   | j   |     | k   |     |     | n   |
| --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |     |     |     |


```
calculate 2d array of lengths beforehand
memo = dict of string : int 
"0 0" : 5
maps mins for any coord
paths = str : int[n-1]

split(table, sj, sk, minPath):
	// base cases
	sum = table[sj, sk]
	if sum  < 0:
		return null
	if sj or sk  == n-1:
		return sum
	
	min;
	if (str(sk+1 + " " + sk)) not in memo:
		min = split(sk+1, k)
	else:
		min = memo[-]
		
	gotk;
	for k = sk+2; k < n-1; k++:
		if (str(sk+1 + " " + k)) not in memo:
			try = split(sk+1, k)
		else:
			try = memo[-]
		if try != null  && try < min:
			min = try
	
	min = min + sum
	
	if (sj + " " + sk) not in memo:
		memo[str(sk+1 + " " + k)] = min
	
	return min
	
```

### Example
Must break before the first line goes above maxLen
*start: 0*
Call me Ishmael. Some 
1. *leave on this line*
	*start: 1*
	Call me Ishmael. Some
	2. *leave on this line*
		Call me Ishmael. Some 
		*start: 2*
		3. *leave on this line*
			Call me Ishmael. Some
		3. *new line*
			Call me Ishmael. 
			Some 
	2. *new line*
		Call me 
		Ishmael. Some 
		*start: 2*


1. *new line*
	Call 
	me Ishmael. Some 
	*start: 1*
	2. *leave*
		Call 	
		me Ishmael. Some 
		*start: 2*
		3. *leave*
			Call 	
			me Ishmael. Some 
		3. *beaks*
			Call 	
			me Ishmael. 
			Some 
	1. *break*
		Call 	
		me 
		Ishmael. Some 
		*start: 2*
	
	
