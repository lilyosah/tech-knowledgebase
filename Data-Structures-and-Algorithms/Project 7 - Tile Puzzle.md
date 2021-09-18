# 7 Tile Puzzle

---

#algo/project 
##### Due: 04-02-2021
- [Class Notion page](https://www.notion.so/Data-Structures-and-Algorithms-2dc17465f862455b86e8d1051ee41539)
- [Description](https://www.notion.so/HW7-Tile-Puzzle-4c0a81caf4d742a381b99a1d314b0c86)
- [ ] Done
- [ ] Submitted

Related:
--- 


## To-do:
- [x]  Plan out Class Board
- [ ]  Go to open hours, make sure this is actually working before
- [x]  Plan out Algorithm
- [x]  Implement
	- [ ]  If I have space issues try representing the board as a 1d list instead of 2d?
- [ ]  Submit

---

## ❓ Problems I'm having:
- for some reason in the new board constructor even though I'm cloning prevboard.state on line 40 the state of prevboard is being changed to what the new board I'm making is being changed to

## Problem Description:
Input: $n$x$n$ 2d array representing a puzzle board.
- 0 is a blank space
Output: String of the characters L, R, D, U which represent the shortest path that things can be switched into the blank space to result in a properly ordered board. 

You can find the shortest distance by using the A* algorithm


### A* Algorithm
A pathfinding algorithm that evaluates possible moves in an order based on their **heuristic distance estimates**, which tell us how good a particular move might be. We consider possible moves in increasing order of score because we're looking for the minimum. 

Keep track of two collections of board states:
1. [[Set]] Boards we've already evaluated
2. [[Priority Queue]] Boards we haven't considered and are one more away from a state that we have already evaluated (is in the first set)

For each board keep track of the sequence of moves you made to get there from the start so we can process the heuristic distance estimate

Initially: 
- 1 is empty
- 2 contains the puzzle's starting state

Repeatedly:
- Take the board from set 2 with the **lowest heuristic distance**, $B$
- If $B$ is the goal, return string
- Else add $B$ to the first set 
	- For each possible moves you might make next from $B$:
		- If the move creates a board we have already evaluated (in set 1), disregard
		- Else, add to set 2
		

#### Heuristic distance estimate (HDE)
: The sum of the actual number of moves it took to get from the starting state to to the current board and the Manhattan distance

==Manhattan distance:== Measures a lower bound of the number of moves needed to get to the final state / the distance between this board and the final. 
- The distance is the sum of the distances of each tile from where it belongs

##### Ex:
Current:

|     |     |     |
| --- | --- | --- |
| 2   | 1   | 3   |
| 5   | 4   |     |
| 6   | 7   | 8   |

Goal:

|     |     |     |
| --- | --- | --- |
| 1   | 2   | 3   |
| 4   | 5   | 6   |
| 7   | 8   |     |

Distance

| Tiles:     | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Distances: | 1   | 1   | 0   | 1   | 1   | 3   | 1   | 1   |

sum = 9


## Ideas:
### Data Structures:
- [[Priority Queue]] to store boards in set 2 because you repeatedly need the boards with the lowest HDE
- A [[Set]] to store boards that I have  already looked at
- A `Class Board` that I implement to represent board states
- A [[Map]] which maps the moves to how the x and y value **of zero** should be changed
	- {D:[0, 1], U: [0, -1], L: [-1, 0], R: [1, 0]}

#### Class Board
##### Instance Vars
1. Index of zero 
	- idx = [x,y]
2. 2d array of board state

| x, y | 0   | 1   | 2   |
| ---- | --- | --- | --- |
| 0    | 1   | 2   | 3   |
| 1    | 4   | 5   | 6   |
| 2    | 7   | 8   | 0   |

#❓ *do the boards always contain sequential numbers?*

3. String of L, R, D, U characters which represents the path taken 
	- ""
4. HDE which is the sum of len(path) and the Manhattan distance 
	- int
5. Manhattan distance 
	- int

##### Methods
###### Constructor 1 (board1 (old board),  move, zeroMoveMap) 
Get array of how zero value will change with the move: 
`coordcoordChange = map.get(move)`


1. Set new zero coordinate:
```
this.zidx = board1.zidx
this.zidx[0] += coordChange[0]
this.zidx[1] += coordChange[1]

```

Get num that will be switched into zero (this.zidx is set to this location but the zero hasn't been placed here yet)
`num = this.state[this.zidx[0]][this.zidx[1]]`

*this.zidx: new z, old num
board1.zidx: old z, new num*

2. Set new Manhattan distance: 
`updateMD(board1, num)`

3. Set new path:
`path = board1.path + move`

4. Set new HDE:
`HDE = this.path.length() + this.MD`

5. Set new state:
```
this.state = board1.state

// this.zidx: new z will be here, coord of old num on board1
// board1.zidx: on new board, the coord of the new num

// put new num in board
this.state[board1.zidx[0]][board1.zidx[1]] = num
// put zero where zidx is set to
this.state[this.zidx[0]][this.zidx[0]] = 0

```


###### UpdateMD(board1, num)
- Make this.MD the value of board1.MD and changed by the move
```
// Should start out as the same
this.MD = board1.MD 

// this.zidx: new z, old num
// board1.zidx: old z, new num

// Get coord of where this number is supposed to be
ideals = idealCoord(num)
idealX = ideals[0]
idealY = ideals[1]

// coord of num after the swap. Swapping to where 0 used to be
newX = board1.zidx[0]
newY = board1.zidx[1]

// coord of num before the swap (this.zidx has already been changed at this point)
oldX =  this.zidx[0]
oldY = this.zidx[1]

// this is moved to incrementMD in my code---
int xOldDist \= Math.abs(oldX \- idealX);
int yOldDist \= Math.abs(oldY \- idealY);
int xNewDist \= Math.abs(newX \- idealX);
int yNewDist \= Math.abs(newY \- idealY);

if (yNewDist < yOldDist) {
	this.MD\--;
} else if (yNewDist \> yOldDist) {
	this.MD++;
} else if (xNewDist < xOldDist) {
	this.MD\--;
} else if (xNewDist \> xOldDist) {
	this.MD++;
 }
// block end ---
```


###### setMDforBoard()
```Java
MD = 0;
n = this.state[0].length
for (int x = 0; x < n; x++) {
	for (int y = 0; y < n; y++) {
		if (this.state[x][y] != 0) {
			MD += oneMD(x, y)
		}
	}
}

return MD

```

###### oneMD(x, y)
calculate the MD of one number in this board
```
// Get coord of where this number is supposed to be
num = this.state[x][y]
ideals = idealCoord(num)
idealX = ideals[0]
idealY = ideals[1]

return Math.abs(x - idealX) +  Math.abs(y - idealY))

```

###### int\[] idealCoord(num)
return the ideal coord for one number in this board
```
n = this.state[0].size
if num == 0:
	return [n - 1, n - 1] 
	
x = (num -1) // n
y = (num - (x*n)) - 1
return [x, y]
```

###### int\[]\[] getIdealState()
return 2d array representing the ideal state of this board
```
idealS = int[this.state[0][1].size][this.state[0].size]

for (int x = 0; x < this.state[0][1].length; x++) {
	for (int y = 0; y < this.state[0].length; y++) {
		num = this.state[x][y]
		idealC = this.idealCoord(num)
		idealS[idealC[0]][idealC[1]] = num
	}
}

return idealS
```


###### Constructor 2 (start int[])
1. Set path: ""
2. Set zidx: must find
3. Set state: start
4. Set MD: this.MD = calcMDforBoard()
5. Set HDE: this.MD

###### Implement comparable
- Compare by HDE

###### Implement .equals
- Equals is same board state and same HDE (needs to be this for set1, should make another state comparison function so you can compare with the ideal board)

###### sameState(stateArray)
return true if they have the same state
`return Arrays.deepequals(stateArray, this.state)`


###### makeMove(move, movemap)
- If the move is possible, return a new board with updated
	- state
	- path
	- manhattan distance
	- HDE 
- If the move is not possible return `NULL`

To implement:
- If MoveValid(board, move)
	- Instantiate new board object with constructor 1 and the move you want to make
- Else return `NULL`

###### boolean MoveValid(board, move, moveMap)
- checks if the move is valid. Move can be made if the number around the zero can move the direction specified into the 0 space (so if D is passed look at element above 0)
```

tentativeX = board.zidx[0] + moveMap[move][0]
tentativeY = board.zidx[1] + moveMap[move][1]

return (tentativeX >= 0 && tentativeX < board.state[0][1].size)&& tenttive Y >= 0 && tentativeX < board.state[0].size

```


### Algorithm Description:
Repeatedly:
- Take the board from set 2 with the **lowest heuristic distance**, $B$ (lowest)
- If $B$ is the goal, return string
- Else add $B$ to the first set 
	- For each possible moves you might make next from $B$:
		- If the move creates a board we have already evaluated (in set 1), disregard
		- Else, add to set 2

```
init moveMap
init checked [[Set]] of Boards that are already checked
init toCheck [[Priority Queue]]  of boards that are one move away from this
toCheck.add(board)

int[][] ideal = board.getIdealState

while ?:
	lowest = toCheck.poll()
	if lowest.sameState(ideal):
		return lowest.path
	else:
		checked.add(lowest)
		for move in moveMap:
			Board moved = this.makeMove(move, movemap)
			if moved != null && !checked.contains(moved):
				toCheck.add(moved)
```
