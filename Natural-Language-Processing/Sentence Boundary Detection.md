# Sentence Boundary Detection
%%
#NLP 
#concept
%%
**Related:**
-  

---

: Determining the start/end of a sentence
- End with a period, exclamation point, etc. 
	- **Ex: ✏**  `! U.S.` is not a sentence 

## [[Machine Learning#Supervised Learning]] approaches
: Comparing the output with given examples

### SpaCy Sentencizer
A rule-based algorithm for [[Python]]
- Periods following non-abbreviations are assumed sentence boundaries

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
- Uses [[Machine Learning]] so abbreviations must be learned to be recognized
	- [[Machine Learning#Unsupervised Learning]]?
- Used to determine possible abbreviations 
	- **Ex: ✏**  U.S.
- Abbreviations should always end on a final period

##### Heuristics
- Liklihood ratios
- Length of word
- Number of periods
- Penalty

## Text Transformations
- [[Text Normalization|Pre-processing words]] is done to make them more simple 
	- **Ex: ✏**  Punctuation removal, lower-case casting, number handlers
- After processing, the words are called tokens because they may not exactly be words anymore
	- **Ex: ✏**  `.` may be considered a token
- Tokens may also be [[N-grams and Q-grams|n-grams or q-grams]]

 ![[Herdan's, Heaps' Law]]