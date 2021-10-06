# Supervised Machine Learning
#📥 
%%
#topic
#concept

**Related:**
-  

%%

- Have a data set of input observations, each associated with some correct output ("supervision signal")

Representation:
- $R$: vector the objects are in 
- $d$: length of the array/vector
- $N$: number of pairs? #NLP/❓ 
- $x \in R^d$
- $y \in C$ where $C = {c_1, c_2, ... c_l}$ (the pre-defined classes)
- $D$:  ${(x_i, y_i) | i \ 1, ... , N}$ (each input with it's correct class) #NLP/❓ 

**Ex: ✏**  150 data sets with 4 numbers (iris measurements) that you're putting into one of three classes implies: $D \in R^{150x4}, y \in C^150$ where $C = {1, 2, 3}$

Function $m$ takes an object and turns it into a vector of data
- Depends on how your represent it. May use the dimensions, etc. 

#### Applications
Both use [[Probability]]

##### Classification
[[Text Classification]]
- For an input $x$, and a fixed set of output classes, return a predicted output in from that set

==Probabilistic classifier:== In addition to outputting the most likely class, outputs the probability of it

$y_i$ within 

##### Regression
$y_i$ within $R$
Where does this thing best fit