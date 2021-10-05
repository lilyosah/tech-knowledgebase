# Collocations
%%
#NLP
#concept
%%
**Related:**
-  [[N-grams and Q-grams]]
-  [[Hypothesis Testing]]

---

: Statements of the customary placements of that word
- The meaning of the  expression does not equal the sum of the parts
- **Ex: ✏**  `"kick the bucket"`

**Applications** 
- Natural language generation to make expression as human as possible
- Parsing: Grouping collocations together

## Methods
### Counting
Simplest method is to count frequency: If two words occur together then they might be a collocation

#### Steps
1. Tokenize
2. Each token corresponds to a word
3. Count

### [[N-grams and Q-grams|N-grams]]

```Python
# Bigrams
T = []

for i in len(words)-1:
	T += (words[i], words[i+1])
	
# N grams
# Basically the above but with range using double for loop so you can get all combos of ranges

```

**Results:**
- This code just groups common words and does not give you collocations
- Not very informative
- Most words are infrequent 

### Other Possible Approaches
- Statistical testing
- [[Hypothesis Testing]]

