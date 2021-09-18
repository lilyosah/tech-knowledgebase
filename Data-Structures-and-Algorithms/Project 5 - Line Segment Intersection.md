# #5 - Line Segment Intersection

---

#algo/project 
##### Due: 03-05-2021 #week/week-6 
- [Class Notion page](https://www.notion.so/Data-Structures-and-Algorithms-2dc17465f862455b86e8d1051ee41539)
- [Description](https://www.notion.so/HW5-Line-Segment-Intersection-6e3f86207fec409882611330cb8f500f)
- [ ] Done
- [ ] Submitted

Related: [[Tree]] [[Data Structures]]

--- 


## To-do:

- [x]  Plan algorithm
- [x]  Implement
- [ ]  Improve efficiency
- [ ]  Submit

---

## Problem Description:
Given the starting and end points of horizontal and vertical lines ad doubles, print the `x` and `y` coordinates of all intersection points.
- Given code to parse an input file where lines are specified by their starting and end coordinates like `x1 y1 x2 y2`, will need to decide which data structure to put these in

## Ideas:
### Data Structures:
- DS to store coordinates (should do sorted by $x$ coords so going from left to right is easy)
	- Maybe a `HashSet<ArrayList<Double>>` where the keys are $x$ coordinates and the values are ArrayLists of All the Y coordinates at this point
	- `TreeMap<ArrayList<ArrayList<Double>>>` since they should be sorted
		- [TreeMap Java Docs](https://docs.oracle.com/javase/7/docs/api/java/util/TreeMap.html)
- `TreeSet<Double>` to store $y$ coordinates of active horizontal lines  (there won't be duplicates so set should be fine)
	- [TreeSet Java Docs](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/TreeSet.html)

### Algorithm Description:
1. Parse line segments from left to right
2. Check all coordinates with that $y$ value
3. If a segment is horizontal (same $y$ coords):
	- When it starts, put the $y$ coordinate in a BST
	- When it ends (you hit a $y$ value that is already in the BST), remove the $y$ coordinate from the BST
4. If the segment is vertical (same $x$ coords):
	- Search the BST for all shared $y$ coordinates in an active horizontal lines, if present print the point of intersection
		- The SubSet function should be helpful for this (find subset of coordinates where Y values is between the lower and higher coordinate) if they are ordered by $y$ coordinates in any DS 

Needs:
- Need to be able to search for a range of coordinates between 2 $y$ values to find intersecting horizontal lines (TreeSet should be fine for this)
- Need to be able to store coords ordered based on $x$ values, can be multiple with the same x value
	- TreeMap? `x vals: ArrayList<Y values at this coord>`
		- Like `2:[ [3], [5], [8, 7] ]` where 3, 5, are $y$ coordinates of  

### Pseudocode

```

For x value in xValsTreeMap:
	ys = xValsTreeMap[x]
	for yVals in ys:
		#figure out if horizontal or vertical
		# if stored in arraylist thing checking size of y val pairs will give horizontal / vertical
		# horizontal
		if (yVals.size() == 1) 
			if yVal[0] not in horizontals:
				horizontals.add(yVal)
			else:
				horizontals.remove(yVal)
		# vertical
		else:
			# get sublist of x vals from treeSet withing this yval range
			horizontalLines = horizontals.SubSet(yvals.min, yvals.max)
			for horizontalY in horisontalLines:
				print(x, horizontalY)
			
				
			
	


```


```

For x value in allX:
	if there are horiztontal values at this x coord:
		for hYval in horizontalValues:
			if hYval is in activeHorizontals:
				if horizontalsValues.count(hYval) == 2
					// print hxh intersections
					print coordinate pair
				else
					toRemove.add(hYval)

			else
				activeHorizontals.add(hYval)
	
	double start
	double end
	if there are vertical values at this x coord:
		for i in range (0; i+= 2; i < verticalyvals.size()-1):
			start = arrayYvals[i]
			end = arrayYvals(i+1)
			activeHinThisRange = activeHorizontals.subset(start, end)
			
			// print hxv intersections
			for yInRange in activeHinRange:
				print coordinate pair
				
			// vxv intersection
			if i < verticalyvals.size()-2 and end == arrayYvals(i+2) and !activeHInThisRange.contains(end)
				print coordinate 
				

				
	while toremove is not empty
		remove from toRemove
				


```