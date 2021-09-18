# 09-07-2021 Title

---

#📥
Class: #NLP
Week: #week/week-3
Tags: 
Related:

---

## Collocations
: statements of the customary placements of that word
- The expression does not equal the sum of the parts
- Ex: "kick the bucket"
- Applications: 
	- Natural language generation to make expression as human as possible
	- Parsing: Grouping collocations together

Simplest method is to count frequency: If two words occur together then they might be a collocation
1. Tokenize
2. Each token corresponds to a word
3. Count

Another method:
### Bigrams

```Python

T = []

for i in len(words):
 T += (words[i], words[i+1])

```


N grams
Basically the above but with range using double for loop so you can get all combos of ranges

Results:
- This just groups common words, does not give you collocations.
- Not very informative
- Most words are infrequent 

Possible approaches: 
- Statistical testing
- Hypothesis testing 

### Hypothesis Testing 
Formal definition:
- H0: null hypothesis
- H1: alternate hypothesis, you have enough evidence to reject H0

Can hypothesis testing be used to find collocations 