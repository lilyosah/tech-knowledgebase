# 10-05-2021 Title

---

#📥
Class: #NLP 
Tags: 
Related:

---

## Exam
[[Wald Test]]
[[Herdan's, Heaps' Law]]


### Bernoulli
$p$

### Normal
Gaussian and normal distribution are the stats bellcurve, normal distribution

$M(\mu, \sigma)$

$\mu$ is the line in the middle of the standard deviation bell curve 
$\sigma$ are the standard deviations along the x axis 

- Two values tell you everything you need to know in normal distribution, $\mu$ and $\sigma$. Therefore $\mu$ and $\sigma$ are the two parameters needed when dealing with normal distribution?

### Bigrams
$P(zx|xy)$ means $zx$ follows $xy$.  Given $xy$, what is the prob $zx$ follows it

What about a 3-gram?
$P(w_i|w_{1-2}w_{i-1})$

q-grams: consonants
n-grams: words

### Classification Problems
(language models )

$X = {(x_1, y_1), (x_2, y_2) ... (x_{100}, y_{100})}$
$y$: classes. 
$y_i \in {1, 2, 3}$
$x_i = R^{10}$ *every $x_i$ is a vector of 10 elements*
A naive Bayes with Gaussian distribution is trained. How many parameters (for the normal distribution) are estimated?
for each class, for each dim in vector, calc each parameter 
$3 (y_i) * 10 (x_i) * 2$ (normal)

$(30 + 30) 60$ because each $y_i$ has 3 classes, each $x_i$ has 10 elements 
- Multiply by 1 for bernoulli, for normal, 2
- But bernoulli has 2 classes
- Normal has any number of classes



