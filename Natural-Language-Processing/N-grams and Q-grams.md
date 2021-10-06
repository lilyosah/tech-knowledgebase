# N-grams and Q-grams
%%
#NLP 
#concept
**Related:**
-  [[Language Models]]
-  [[Collocations#N-grams and Q-grams N-grams]]

%%

## N-grams
Looking at the probabilities of seeing small groupings of words one after another
- Breaking a string of words into string of $n$ number of words
- Used for text prediction, etc.
- Words are broken into groups based on their original ordering
**Ex: ✏**  `Good morning friends` --> `{Good morning, morning friends}`

### Using N-grams
$P(w|h)$: The probability of a word $w$ occurring based on history $h$

**Ex: ✏**  Probability that the next word is learn
$A = \text{learn}$
$B = \text{you still have much to}$
$$
P(\text{learn}|\text{you still have much to}) 
= {count(\text{you still have much to learn}) \over count(\text{you still have much to})}
$$

> ❗ Could compare occurrences of a very large corpus but this doesn't work very well because new sentences are created all the time and **entire sentences are unlikely to repeat much,** for this reason usually n-grams of $n = 2$ or $n = 3$ are more often used.


After applying the chain probability rule: 
$$
\text{Sentence prob: }\displaystyle\prod_{k = 1}^n P(w_k|w_1:k-1)
$$
*Multiplying the probability of each sentence* 

Where $w_k$ is the $k$th word. This lets you approximate the history using just a few of the words before.

==Bigram:== Looking one word into the past, $n = 2$  

==Extrinsic evaluation:== Using data models in an application and measuring how much it improves
==Intrinsic evaluation:== Measure the quality of a model independent of an app

## Q-grams 
: Breaking a string of words into string of $q$ number of characters
**Ex: ✏**  `Good morning` --> ` {Goo, ood, od, d m, mo, mor,...}`

