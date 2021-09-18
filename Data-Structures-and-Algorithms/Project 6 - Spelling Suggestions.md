# 6 Spelling Suggestions

---

%% #algo #algo/project %%
##### Due: 03-19-2021 #week/week-8 
- [Class Notion page](https://www.notion.so/Data-Structures-and-Algorithms-2dc17465f862455b86e8d1051ee41539)
- [Description](https://www.notion.so/HW6-Spelling-Suggestions-83a778f712d144aea1a9ff597b346632)
- [ ] Done
- [ ] Submitted

Related: [[03-04-2021 PSS Tries]]

--- 


## To-do:

- [x]  Plan algorithm
- [ ]  Implement

---

## Problem Description:
Implement `public HashMap<String, Integer> suggestions(String target, int dist, int max)`
- Given a target string, a maximum distance accepted and a max number of words to add, return a map of the max number most similar words to the given target, with the string as a key and it's distance as the value.
	- target is lowercase and alphabetic
	- if max is less than the total number of options within the trie, the ones closest to the target should be included
		- if max is negative all options should be included

Levenshtein distance: the minimum number of operations to turn one string into another using the following transformations:
	- insert a single char
	- delete a single char
	- substitute one character for another

 <br/>

## Ideas:
### Algorithm Description:

#### Data structures
[[Map]]
[[Tree]]

1. Idea 1, compare one index
	- recurse through the tree
		- Pass: TargetIndex, prefix/currentWord, node, map
		- keep track of the number of changes you have made in traversal from the original path
		- keep track of what index you are "on" in the target string, so that if you add or delete some char in the new word every letter after that point isn't counted as a change.
			- Ex: target: cat
			- Assume the changes are made on the previous recursion frame so this one is just "reacting" to changes and counting them
				- t: cat, newWord: bat (substitution)
					- changes++ (because [targetIndex (0)] != currentNode.letter)
					- targetIndex++ (1)
				- going through a increments targetIndex (2), no change
				- t: cat, newWord: bai (adding)
					- changes++
						- if you find t next it should not be counted as a change
					- ==LEAVE TARGET INDEX AS LAST INDEX (2)==
				- t: cat, newWord: bait (adding)	
					- no change because target[targetIndex (2)] == currentNode.letter (t)
					- ==LEAVE TARGET INDEX AS LAST INDEX==
				- t: cat, newWord: baits
					- change++
			- Ex: target: bait
				- t: bait, newWord: bat
					- targetIndex = (2)
					- changes++
					- targetIndex++
		- Base case:
			- changes > distance || node.children == null
				- return
		- Else:
			- Check if changes should be incremented
				- if target[targetIndex] != node.letter, changes++
			- Check the current path is a word and add to map
				- if a word and not in the map, add to the map at this distance. If in the map, only add if this new distance is shorter than the current distance in the map
			- if targetIndex < target.length -1, targetIndex++
			- Call function recursively on all the children of this node
2. See if letter in word and correct place
	- Do you actually only need to check from the letter before in currentWord? I guess everything before that point would have been checked already
		- if target contains letter being added
			- find closest letter (cl) before this one that was in target ==and comes *before* added in word.==
				- cl is the last letter from the word.substring(0, length-2) in the target (cl is first occurrence in target of the last thing before added in word, last is the index of the last occurrence of the added letter in target)
					- if you can't find one ?
						- if len?
						- return -1
					- if you do find one
						- If index of cl and last occurrence of letter in target are the same ==OR== last < cl
							- if <= len return 0
							- else return 1
						- else:
							- make substring of target from (cl:this letter (==last occurrence==)) 
							- if sub empty
								- you are not missing any letters, return -1?
							- if it is not empty, if word <= length return 0, if not 1?
		- If does not contain letter
			- if len(word) <= len(target)
				- if changes == 1
					- return 1
				- else return 0
			- else return 1
		
	ex:
		ever
		4 s -> not in target and <=  length, 0
		3 se -> in word, look for cl in "ever" from "s". no cl, -1
		3 see -> e in word, look for cl in "ever" from "se". cl is previous e. substring in target is "v"  (bc look from first occurrence to last). Not empty and <= length, 0
		3 seem -> m not in word and <= length, 0
	ex2: 
		ever
		3 r -> in word, look for cl in "ever" from "". no cl, -1
		3 ro -> not in word and <= len, 0
		3 roa-> not in word and <=len, 0
		3 roar -> in word, look for cl in "ever" from "roa". cl is previous r. index of cl and last occurrence of letter are the same, 0
	ex3: 
		ever 4
		3 v -> in word, look for cl in "ever" from "". no cl, return -1
		2 ve-> in word, look for cl in "ever" from "v". cl is v. substring in target is "". substring is empty, -1 
		1 ver -> in word, look for cl in "ever" from "ve". cl is e. substring in target is "". substring is empty, -1 
		2 vers -> not in word, <= len, but len - changes == 0 so 1???
		3 verse -> in word, look for cl in "ever" from "vers". cl is r. cl > last and > len so 1
	ex 4:
		ever
		3 e -> in word, look for cl in "ever" from "". no cl, -1
		ev -> in word, look for cl from "e". cl is first e. target substring is ""
	ever
	v 3 ✔
	ve 2 ✔
	ver 1 ✔
	vers 2
	verse 3 ✔ (working correctly but dependent upon previous step)

	0 if changes < len?
	1 otherwise

	```
	// changes starts as len(target)

	//new base case: 
	if changes > dist and len(currentWord) > len(target) 
		return


	if last char in currentWord in target:
		if in correct place:
			// see if in correct place, are not too many of the letters
			// see if any letters before this one in original word are in the second word and if they come before this one being added

			int indexOfLetterInTarget
			for letter in current word until the letter being added:
				if letter in target and target.indexOf(letter) > indexOfLetterInTarget:
				if (len(current) > len(target))
					changes++
				break
			same with other side

			// see if any letters after are in currentWord and if they are, come after this letter  
			// may be several if there are several letters
			if changes > 0:
				changes--
		else if len(current) > len(target):
			changes++
	// word not there and current is longer than target
	else if len(current) > len(target):
			changes++
	```
3. Use alg. I found online :( [cheater cheater](https://norvig.com/spell-correct.html)
	```
	// deletion
	// delete current letter
	// remove the letter that was just added????
	findDiff(word(:last), changes + 1);
	 	
	for each child:
		// insertion, pass the word plus the next child
		// get rid of target as you go through 
		findDiff(word + child, changes + 1)
		
		// substitution
		
		// no change at this letter
		findDiff(word + target letter)
	
	if is word and changes < max, add to dict
	
	
	```


### Debugging
s 4
   se S: ever
   se S: ever
   substring contains e: true
   2
se 3 
   see S: ever
   see S: ever
   substring contains e: true
   see S: ver
   substring contains e: true
   2
see 2 
	==This should stay as 3 and not decrement. Should reach flag 1 inside for loop, should look for substring and not find e?==
seem 2
		
---

❔ I think you have to add concatenate the strings and pass those to recursive functions to add them to the map (newWord/prefix)... 
- This will be a slight space disadvantage, cost of passing strings
- can you do it as you return? I don't think so because each function would be returning several strings 



#### Ideas for handling if if you only return a certain number of items 

1. Two versions of the recurse function
	1. If max is negative, call the normal version that does not add to a second, ordered hashmap 
		- After, return the normal HashMap
	2. else: call the second version which also maps changes: `HashMap<Integer, HashSet<String>>`
		- This version also adds items to a hashmap that orders the strings by their changes
			- You can have another base case that checks if the number of items with one change is more than the max
			- This could not be terrible space-wise because if the size of map1 is larger than the max, before adding something to the tree you could see if the changes of the string are larger than the largest key, if they are then do not add 
		- After, iterate through the ordered keys (changes) and move an appropriate number into the final map to return

2. Iterate through the map after you recurse through the trie
	- Have to iterate through the strings 
		- You can get a collection view of the values, but how would I map these back to the keys 
	- 


 <br/>

### Pseudocode
```

if changes <= distance:
	if


```
