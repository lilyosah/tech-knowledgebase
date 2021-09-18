# Language Models and N-grams
#topic
#concept
**Related:**
-  

---

==Language models==: Assign probabilities of occurrences to sequences of words


Conditional probability
$P(A|B) = {P(A, B)}/{P(B)}$

$P(.|B)$ satisfies the axioms of probability 


## N gram
$A = learn$
$B = you still have much to$
$P(learn|you still have much to) = {count(you still have much to learn)}/{count(you still have much to}$
probability that the next word is learn
$P(w|h)$: The probability of a word w occurring based on history h
- Could compare occurrences of a very large corpus
${C(\text{"the dog went out"})}/{C(\text{"the dog went"})}$
- This doesn't work very well bc new sentences are created all the time


After applying the chain probability rule: 
n
∏  P(wk |w1:k−1)
k=1
Probability of the sentence. Multiplying the probability of each sentence 
The probability of encountering the concatenation of ech of the words 
N gram: Looking at probabilities of seeing small groupings of words after one another
(Hi my) (my name) (name is)


Where wk is the kth word. This lets you approximate the history using just a few of the words before.

Bigram: Looking one word into the past 

Extrinsic evaluation: using data models in an application and measuring how much it improves
Intrinsic evaluation: measure the quality of a model independent of an app