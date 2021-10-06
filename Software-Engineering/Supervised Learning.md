# Supervised Learning
#📥 
%%
#coding 
#concept

**Related:**
-  [[Machine Learning]]
-  [[Text Classification]]

%%

- Have a data set of input observations, each associated with some correct output ("supervision signal")

Representation:
- $R$: vector the objects (data) are in 
- $d$: length of the array/vector
- $N$: number of data points 
- $x \in R^d$
- $y \in C$ where $C = {c_1, c_2, ... c_l}$ (the pre-defined classes)
- $D$:  ${(x_i, y_i) | i \ 1, ... , N}$ (each input with it's correct class) #NLP/❓ 

**Ex: ✏**  150 data points ($N$) with 4 numbers each ($d$) (iris measurements like \[2.1, 3.4, 2.3]) that you're putting into one of three classes implies: $D \in R^{150x4}, y \in C^{150}$ where $C = {1, 2, 3}$
- 📝 This $R$ is not the same as the one the data is from

Function $m$ takes an object and turns it into a vector of data ($D$? #NLP/❓ )
- Depends on how your represent it. May use the dimensions, etc. 

#### Applications
Both use [[Probability]]

##### Classification
[[Text Classification]]
- For an input $x$, and a fixed set of output classes, return a predicted output in from that set
- $y_i$ within $C$

==Probabilistic classifier:== In addition to outputting the most likely class, outputs the probability of it


##### Regression
- $y_i$ within $R$
Where does this thing best fit