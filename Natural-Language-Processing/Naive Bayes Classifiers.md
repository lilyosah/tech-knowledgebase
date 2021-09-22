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

$$\hat{c} = {argmax P(c|d) \atop {c \in C}} = {argmax P(d|c)P(c) \atop {c \in C} }$$

Liklihood of the document: $P(c|d)$
Prior probability: $P(c)$