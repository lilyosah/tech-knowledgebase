# 09-22-2021 Title

---

Class: #NLP 
- [Description](https://moodle.colgate.edu/mod/page/view.php?id=530672&inpopup=1)
- [ ] Done
- [ ] Submitted

Related notes:
Tags:

--- 

## Problem
Improve the [[Python]] [Spacey Sentencizer](https://spacy.io/api/sentencizer).

## Things we know
- Acronyms
	- `"I live in the U.S. and my name is Mairo"` -> 1 sentence, says it's 1✔
	- `"I live in the U.S. My name is Mairo"` -> 2 sentences, says it's 1 ❌
		- We could check if the next sentence starts with a capital
		- He has two lines that check whether the token is a punctuation point, if not but has a period in it then `in_punct_chars` then it's an acronym. The commented out code ends the sentence if it's an acronym. We would need to add to this to see if this is true and the next word starts with a capital letter, make this a sentence boundary. Not just every case, just when next starts with a capital
- Tokenizes acronyms, even if they're really weird and not real, correctly
	- `U.S.A.` is tokenized as one
	- `L.M.A.O.` is one
	- Does not count them as the end of sentences
- Gradescope:
	- One number is based on how many sentences you submitted
	- (perfetalg - perfectdefault) => 0 means it's the same as the default alg
	- A 1 is weird because it's the opposite of the default alg

## Things we don't know
- Why does `.is_punct` not include commas/ why do they not break up sentences

## Ideas
Add rules to the existing code to catch more cases.
- Ending sentence with acronym - Sort of implemented
	- Problem with the assertion
- Decimal numbers ✔
- Newline 
- Roman numerals
- e.g. an i.e. ✔
- Honorifics ❌
	- `George Sr. brushed his teeth.` -> breaks it into 2, should be one 
	- Thinks `Miss. My name is George.` is 1
	- Things it breaks on: 
		- Sr.
		- Capt.
		- Col.
		- Drs.
		- Lt.
		- Agt.
		- Mx.
		- Misc.
	- One solution: Check if the current token is in this list. If it is and the next token is a period, and the first letter of the following token is lowercase, assume to not be the start of a new sentence. 
		- Problem with this: If it's followed by a proper noun this will be marked as the end of the sentence but there's not an easy way to check if the following token is a proper noun. 
		- Solution: have two sets, one with honorifics, these should not be sentence boundary when the next word is uppercase. Abbreviations should not be sentence boundaries when the next word is lowercase.
