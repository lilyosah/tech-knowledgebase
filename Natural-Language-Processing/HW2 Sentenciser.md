# 09-22-2021 Title

---

Class: #NLP 
- [Description](https://moodle.colgate.edu/mod/page/view.php?id=530672&inpopup=1)
- [ ] Done
- [ ] Submitted

Related notes:
Tags:

--- 

## Things we know
- Acronyms
	- `"I live in the U.S. and my name is Mairo"` -> 1 sentence, says it's 1✔
	- `"I live in the U.S. My name is Mairo"` -> 2 sentences, says it's 1 ❌
		- We could check if the next sentence starts with a capital
		- He has two lines that check whether the token is a punctuation point, if not but has a period in it then `in_punct_chars` then it's an acronym. The commented out code ends the sentence if it's an acronym. We would need to add to this to see if this is true and the next word starts with a capital letter, make this a sentence boundary. Not just every case, just when next starts with a capital
- Tokenizes acronyms, even if they're really weird and not real, correctly
	- `U.S.A.` is tokenized as one
	- `L.M.A.O.` is one
	- Gradescope:
		- One number is based on how many sentences you submitted
		- (perfetalg - perfectdefault) => 0 means it's the same as the default alg
		- A 1 is weird because it's the opposite of the default alg

## Things we don't know
- Why does `.is_punct` not include commas/break up sentences

## Ideas
Add rules to the existing code to catch more cases.
- Ending sentence with acronym
- Decimal numbers
- newline 
