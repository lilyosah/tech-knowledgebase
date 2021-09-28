# Naive Bayes Classifiers
#📥 
%%
#NLP 
#concept
**Related:**
-  

%%

Created for [[Sentiment Classification|category classification]]

- Called naive because it assumes the words are in an unordered set, keeping only their frequency

Returns $\hat{c}$ where $\hat{c}$ has the maximum posterior probability given the document 

Lets you break down any conditional probability into  three other probabilities 

$$P(x|y) = \frac{P(y|x)P(x)}{P(y)}$$

After some substitution:

$$\hat{c} = {argmax P(c|d) \atop {c \in C}} = {argmax P(d|c)P(c) \atop {c \in C}}$$

Liklihood of the document: $P(c|d)$
Prior probability: $P(c)$

==Precision:== The percentage of items that the system detected that are in fact positive 
==Recall:== The percentage of items actually present in the input that were correctly identified by the system 

## Coding Implementation
Iris example: 
- Classes: Kinds of Irises
- Variables: Features of each: length, width... etc. 
```Python

from sklean.naive_bayes import GaussianNB

naive = GaussianNB()
naive.fit(D, y)

naive.class_prior_ # Shows info about the classes (kinds of irises)
naive.sigma_

```

Obtaining u from D
In numpy you can use a boolean array to get certain elements from an array


```Python

# Array masking
mask = np.array([True, False, True, False])
a = np.array([1, 2, 3, 4])
a[mask] => array([1, 3])

a == 2 => Array([False True False False])

# Adds them all up
a.sum()

```

Obtaining the standard deviation (o thing symbol raised to the power of two)

Think about having three classes as $D_0, D_1, D_2$

```Python

D0 = D[y == 0]
d0.shape

```

If you have a matrix and you want to add up columns, have to specify which axis you're working on
- Axis 0 is vertical/y
- Axis 1 is horizontal/x

So if we have something of shape (50, 4), Axis 0 is 50 numbers, axis 1 is 4

### Prediction 
Now that we have a model, we can use it for prediction
- `predict` ex
