# 08-31-2021 Basic Text Processing

---

#📥
Class: #NLP
Week: #week/week-2
Tags: 
Related:

---

## Sentences

- Ends with period, exclamation point 
	- ! U.S. is not a sentence 

- Supervised learning approaches: comparing the output with given examples
- Unsupervised learning approaches: 

### Sentence boundary detection
#### spaCy sentencizer
- Rule based alg
```python

require w (array of words)

period = False
start = 0
sentence = [0, 0, ...]

for word in w:
	if period and word not in punctuation:
		sentence[start] = 1
		start = word index
		period = False
	else if word in punctuation:
		period = True
return sentence

```

#### Punkt Sentence Tokenizer
- uses ML so abbreviations must be learned to be recognized
	- Unsupervised learning?
- determine possible abbreviations Ex: U.S.
- abbreviations should always end on a final period
- Periods following non-abbreviations are assumed sentence boundaries

Heuristics: 
- Liklihood ratios
- length of word
- number of period
- penalty

## Words

- \[a-zA-Z0-9]
- Not always straightforward 
- Chars separated by spaces, sometimes? New York?
- Abbreviations, kind of one word? Kind of not 
- Apostrophes, one word?


## Text transformations
- pre-processing words to make them more simple
	- Ex: punctuation removal, lower casting, number handlers
- After that call them tokens bc they aren't all really words after
- Sometimes tokens are q-grams (ex: 3-grams)
	- Ex: Good morning --> {Goo,ood,od ,d m, mo, mor,...}
- Sometimes n-grams (ex: bigrams)
	- Ex: Good morning friends --> Good morning,morning friends
- Subwords
	- Byte-pair encoding 

Ex: TC Tokenizer 

## Herdan's Law / Heaps' Law

$|V|=kN^\beta$
- $V$ = unique tokens or the number of types. Set of all tokens 
- $N$ = number of total tokens


Count() creates dict for counting in Python