# 3 Divide and Conquer

---

#algo 
#algo/project 
##### Due: 02-19-2021 @11:49 pm #week/week-3 
- [Class Notion page](https://www.notion.so/Data-Structures-and-Algorithms-2dc17465f862455b86e8d1051ee41539)
- [Description](https://www.notion.so/HW3-Missing-Combinations-5c202824a48943c3a320b34587eb3907)
- [ ] Done
- [ ] Submitted

Related notes: [[02-11-2021 Divide and Conquer]]

--- 

### To-do:

- [x]  Plan algorithm
- [x]  Figure out how to deal with the sorting aspect
- [x]  Implement it
- [x]  Make sure the runtime is okay?
- [x]  Turn in

---

#### Description: 
- Input: table V of variable combinations that were tested
- Output: list of combinations that were missed

We need a full truth table for $n$ items with two states but some combinations are missing. 

#### Ex: complete truth table 
When $n = 4$ there are $2^4$ (16) rows / tests (two options for $n$ items) 

Row (t)|V1|V2|V3|V4
--|-- | --| --|--
0 | 0 | 1 | 1 | 1
1 | 0 | 1 | 1 | 0
2 | 0 | 1 | 0 | 1
3 | 0 | 1 | 0 | 0
4 | 0 | 0 | 1 | 1
5 | 0 | 0 | 1 | 0
6 | 0 | 0 | 0 | 1
7 | 0 | 0 | 0 | 0
8 | 1 | 1 | 1 | 1
9 | 1 | 1 | 1 | 0
10 | 1 | 1 | 0 | 1
11 | 1 | 1 | 0 | 0
12 | 1 | 0 | 1 | 1
13 | 1 | 0 | 1 | 0
14 | 1 | 0 | 0 | 1
15 | 1 | 0 | 0 | 0

Your job is to write a program that implements an efficient divide-and-conquer algorithm to figure out which combinations are missing.

Your algorithm should ideally use $O(2^n\log k)$ 
table-cell queries of the form  $V(t, v)$, where each query returns one variable setting in one test
$t$: the number of a test $t$, where $0 \leq t < 2^n -k$. In the table above this would be the row #
$v$: the number of a variable $v$, where $0 \leq v < n$. In the table above this is V1-V4

#### VarCombos Methods
- `boolean queryTable(row, var)` : returns whether a variable in a row is true or false
- `int size()` : number of rows (tests)
- `int numVars()` : number of variables (per row)
- `int numMissing()` : number of missing tests

### Running the code:
VarCombos main:
1. Reads the number of variables (n) and the number of missing tests (k) as two integers from the command line to set up the table (if there is a third arg (anything) will print the table using the wacky description)

Repeatedly:
-   Reads two integers $t$ (test) and $v$ (variable) from standard input, prints the boolean returned form the query `queryTable(t, v)`.

### Ideas:
###### Data Structures
- Input is a table of combinations stored as `int[]`
	- each integer represents the an entire for of the table. 
	- Ex: the integer 1 represents the bits `0001` which is interpreted from least to most significant, so `1000`
- Keep track of rows that might be missing with a `Queue<Integer>` just because it has constant add runtime [[Queue]]
- Ultimate output is `boolean[][]` where first array is the missing test and the second is the variable within that test

###### Understanding the number storage system
- Need to know what the bits at any one place are for each number
- It's reversed so a 1 is represented by `100`
- In the first place in the table (V1), if there is a `1`, then the integer:
	- has a `1` in the last place of the bit representation, which means:
		-  it is odd
		-  has $2^0$ which = 1 
- In the last place in the table (V4), if there is a `1` the integer:
	- has a `1` in the first place of the bit representation, which means:
		- It's big, *bigger than half of the others?*
		- At each level if it has a one in that place it will be bigger than half of the others, so either `t[n/2]` should be $n/2$

###### Idea 1 Algorithm Description
Add things from each call to helper to the final queue
1. Call a helper
2. Keep track of: 
	- `variable` (index of row)
	- `rows` that contains rows that you know are not missing at every level
	- At each step calculate `int power = numVars - 1 - variable`
3. If the table was complete there would be $\frac{2^{\text{power}}}{2}$ rows that start with 0, same with 1 
4. Add the rows that have zeros or ones at index `variable` (requires querying for each row) to `Queue<Integer> ones` and `Queue<Integer> zeros` 
5. Recursively call the function on the `HashSet<Iteger>` that is smaller than it is expected to be (or both):
	- How to tell which is missing values: If `set.size()` < $\frac{2^{\text{power}}}{2}$
	- Recursive call: Store what each function returns in a `Queue<Integers>` of numbers from the zero and/or the ones side
		-  For ones: Add the number given by that place value and add $2^\text{power}$ to everything in that set
			```Java
			HashSet<Integers> newOnes = recurse(ones, variable + 1);
			for (num : newOnes) {
				num += Math.pow(2, power);
			}
			
			```
		- For zeros:
			```Java
			HashSet<Integers> newZeros = recurse(zeros, variable + 1);
			```
	- Combine both Queues after the numbers have been added as needed
	-> Alternatively could store everything in one queue but might need to make a new one each call 
	- Return the combined queue
5. Base case is `variable == numVars - 1`   
	- This is when you're looking at the last variable
	- Need to know if you should add zero, one, or both
		```
		if variable = numvars-1:
			ret = hashset
			if collection !contains 0:
				 ret.add(0);
			if collections !contain 1:
				ret.add(1);
			return ret
		```



==**Example:**==
`2, [12, 10, 4, 2, 3, 7, 11, 5, 1, 15, 14, 9, 0, 6, 8, 13]`
*look through for all that start with 1s*
-> there are 8
*look through for all that start with 0s*
-> there are 8
`[]`
`[]`

n = 3
0: 000
1: 001
2: 010
3: 011
4: 100
5: 101
6: 110
7: 111
actual: 0, 1, 3, 4, 5, 7
missing: 2, 6

*variable = 0*
*depth = 2*
0s expected: 4
found: 3
return 0 + recurse (0, 1, 3) (0s at level variable)
	*variable = 1*
	*depth = 1*
	0s expected: 2
	found: 2
	1s expected: 2
	found: 1
	return $2^1$ + recurse (3) (1 at level variable)
		*variable = 2*
		return the whatever this one isnt
		return 0
0 + 2 + 0 => 0 
		


n = 3
0: 000
1: 001
2: 010
3: 011
4: 100
5: 101
6: 110
7: 111
actual: 0, 3, 4, 5, 6, 7
missing: 1, 2

*variable = 0*
*depth = 2*
0s expected: 4
found: 2
return 0 + recurse (0, 3) (0s at level variable)
	*variable = 1*
	*depth = 1*
	0s expected: 2
	found: 1
	return 0 + recurse (0) (0s at level variable)
		*variable = 2*
		*depth = 1*
		return 1
	1s expected: 2
	found: 1
	return $2^1$ + recurse (3) (1 at level variable)
		*variable = 2*
		*depth = 1*
		return 0
		
Should return 0 + 0 + 1
and 0 + 2 + 0 
as two different numbers but rn they're being added together to get 3


###### Runtime analysis 
*(Should use $O(2^n \log k)$ / 

$O((\text{number of rows expected})*\log(\text{number of rows that are missing)}))$

$T(n) = \text{number of sub-problems}*T(\frac{n}{2})$

table-cell queries)*:
1. Time to sort (maybe this isn't counted because it isn't a query)
2. Time to 


###### Idea 2 Algorithm Description
1. Keep a path array/list that you pass the the recursive funcs, length of 



if variable = numvars-1:
	ret = hashset
	if collection !contains 0:
		 ret.add(0);
	else 
		ret.add(1);
	return ret
		
	

if missing 0s:
	hashset zeros = recurse (zeros)
	add 0s to all those values
if missing 1s:
	hashset ones = recurse (ones)
	add 1s to all those values
add hashsets together 
returnn hashset
	
	for i in vals, add 0