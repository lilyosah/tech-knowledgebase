# 2 Algorithmic complexity Union-Find case study Project

---

##### Due: 02-05-2021 #week/week-1 
#algo 
- [Class Notion page](https://www.notion.so/Data-Structures-and-Algorithms-2dc17465f862455b86e8d1051ee41539)
- [Description](https://www.notion.so/HW1-Maze-Generation-f9429c5c7c114979a1dba79bb5b55984)
- [x] Done
- [x] Submitted

Related notes: [[Algorithmic Runtime]] [[Disjoint Sets]]

--- 


### To-do:

- [x]  Generate maze that is R x C maze cells wide
- [x]  Insert cells into our data structure with the elements all disjoint. This corresponds to all walls being present because each cell is connected to no others.
- [x]  Loop until all cells are connected (count on set returns one)
    - [x]  Pick a random wall
    - [x]  Check to see if the cells on either side are part of the same set, if not, union the sets
    - [x]  Delete that wall
- [ ]  Break into helpers

---

### Ideas:

- DS to store cells and walls:
    - Hasmap to store cell and its walls:
        - arraylist of two ints is the cell  : hasmap of a 1 (right wall present) and 0 (bottom wall present)
    - Disjoint set to hold connections

1. We loop until all cells are connected (a query to the union-find structure):
    1. Pick a random wall.
    2. Check to see if the cells on either side of the wall are part of the same set; if not, we *union* their sets together to record that those cells, *and all the cells they are connected to*, are now connected.