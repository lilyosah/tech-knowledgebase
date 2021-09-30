# Text Classification
#📥 
%%
#NLP 
#concept
**Related:**
-  

%%

==Text categorization:== Assigning a label or category to an entire text or document
==Sentiment Analysis:== Extraction of sentiment from text
[[Naive Bayes Classifiers]] was created for subject category classification
Most classification is done using [[Machine Learning#Supervised Learning]]

Input -> classifier -> class label category 
- Inputs are texts
- You know all the classes
- If input is not in the correct dimension (vector), must reformat it (function `m`)

## Creating Text-to-Vector Function
==Bag of Word model:== id : token -> N
- Dict to map IDs to a unique token (Like two dicts, keys to vals, vals to keys)
- Alg, each token gets value that is the size of the dict

d (unique tokens) corresponds to max_x id(x)

function delta returns 1 if $i \in id(x) | x \in tokens(text)$, 0 otherwise 
*index\[ID of this token in array] = 1*
m(text) = delta_0(text), delta_1(text)... delta_d-1(text)
**Creates a boolean mask of all of the tokens**


|     |     |     |     |
| --- | --- | --- | --- |
| 0   | 0   | 1   | 0   |

## Naive Bayes with Bag of Word
[[Naive Bayes Classifiers]]
