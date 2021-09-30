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
- Map IDs to a unique token (Like two dicts, keys to vals, vals to keys)