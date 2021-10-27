# 10-26-2021 Title

---

#📥
Class: #NLP
Week: #week/week-
Tags: 
Related:

---

: assigns prbabilities to words such that it is possible to measure the probability of the next word given the history. Sometimes you don't need a prob function and can have a func that sorts tokens st the most probable is first
- Can map 64 chars into 64 dim vector space
	- More parameters => easier to learn something
	- Fewer => faster, testing

$P(w_k|w_1, w_2, ... w_k)$

All words around current token are context. 

**Ex: ✏**  
X = Hi it is rainy
$x^\_ =$ Hi it was rainy

$f_\text{is}(\text{Hi it rainy}) = 1$ *if "is" is in the text* 
$f_\text{is}(\text{Good morning}) = -1$ *if "is" is not in the text*

$f_v$ is a binary classifier that predicts the appearance of word $v$ given a context
$v$ must not be in BoW model [[Text Classification#Naive Bayes with Bag of Word]]

Start with a dataset of texts
Look for emojis
Convert into labeled dataset ([[Supervised Learning]] problem)

Converting a dataset without labels into one with labels is called self-supervised learning 


In the vector you make, each emoji will be represented by a number between -1 and some number above one, it's optimized around 1 though so higher is more likely


## BOW vs ...

$f_\text{BoW} => R^k$ where k is the number of classes
$f_\text{emoji} => R^k$ where k is the number of classes

$(f_\text{BoW}, f_\text{emoji})$
$\text{text (good morning, night)} => [.01, .2, .5, 1.4, 1.0, .3]$
