# Bayes' Rule
#📥 
%%
#topic
#concept
**Related:**
-  [[Probability]]

%%

: Describes the probability of an event based on prior knowledge of conditions that might be related to the event 
> Lets you break down any **conditional [[Probability]]** into three other probabilities 

$$P(x|y) = \frac{P(y|x)P(x)}{P(y)}$$

✨Bayes' theorem was created for [[Text Classification|category classification]]
📝 Called naive because it assumes the words are in an unordered set, keeping only their frequency
- Returns $\hat{c}$ where $\hat{c}$ has the maximum posterior probability given the document 

After some substitution:

$$
\hat{c} = {\text{argmax} P(c|d) \atop {c \in C}} = {\text{argmax} P(d|c)P(c) \atop {c \in C}}
$$

Liklihood of the document: $P(c|d)$
Prior probability: $P(c)$