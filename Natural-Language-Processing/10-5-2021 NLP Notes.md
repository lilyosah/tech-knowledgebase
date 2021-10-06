# 10-05-2021 Title

---

#📥
Class: #NLP 
Tags: 
Related:

---

## Exam
### Wald Test
#🔍 *don't follow this*
If you have an estimation of a parameter $\theta$, then assuming $\hat{\theta}$ is asymptotically normal than the null hypothesis $H_0 = \hat{\theta} = \theta_0$ can be rejected if $|W| > Z_{a/2}$ where $W = {\hat{\theta}-\theta_0}/{\hat{se}}$ where se is the standard error 

- Compute $W$
	- $W$ is like an area under part of a s-dev curve... the probability of the thing??? happening??????

If you want to test a particular parameter to see if it is different from another, hypothesis 0 is that they are equal, H1 is that they are not

$x = {12, 3, 4}$
$x ~ N(mew, sigma)$

**Ex: ✏**  
You have a lot of numbers, just guess that one is the mean, then Wald's test is determining if this is true

#### Applications for NLP
- [[Collocations]]
To tell whether something may be a collocation or not 

Null hypothesis: prob of looking into two words is equal to them being selected independently

$H_0 : \hat{\theta} = \theta_0$ 

Other prob: If you reject it, you are saying that they are not independent. Knowing one of the words will tel you something about the other one

$H_1 : \hat{\theta} \ne \theta_0$

$N$ : number of tokens in a corpus 
$P(w_1 w_2) = P(w_1)P(w_2)$
$\theta_0 = P(w_1)P(w_2)$
$P(w_1 w_2) = {c(w_1 w_2)}/{N}$

### Heap's Law
[[Sentence Boundary Detection]]
$|V| = k{N^b}$
$|V|$ size of vocab
$k$ param
$b$ param
$N$ number of independent values

Q: Can $b$ be equal to one given that $b$ has been trained in a big big big corpus
No, because in a big corpus there are a lot of repeated words. $|V|$ is the number of unique words, so $b$ would have to be like negative or really small so make the eq. equal. $b$ dominates bc it's bigger


### Bernoulli
$p$

### Normal
$M(\mu, \sigma)$

$\mu$ is the line in the middle of the standard deviation bell curve 
$\sigma$ are the 

### Bigrams
$P(zx|xy)$ means $zx$ follows $xy$.  Given $zx$, what is the prob second follows it

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



