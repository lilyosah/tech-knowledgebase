# 10-26-2021 Title

---

#📥
Class: #NLP
Week: #week/week-
Tags: 
Related:

---

: assigns prbabilities to words such that it is possible to measure hte probability of the next word given the history. Sometimes you don't need a prob function and can have a func that sorts tokens st the most probable is first

$P(w_k|w_1, w_2, ... w_k)$

All words around current token are context. 

**Ex: ✏**  
X = Hi it is rainy
$x^\_ =$ Hi it was rainy

$f_\text{is}(\text{Hi it rainy}) = 1$ *if "is" is in the text* 
$f_\text{is}(\text{Good morning}) = -1$ *if "is" is not in the text*

$f_v$ is a binary classifier that predicts the appearance of word $v$ given a context
$v$ must not be in BoW model [[Text Classification#Naive Bayes with Bag of Word]]

