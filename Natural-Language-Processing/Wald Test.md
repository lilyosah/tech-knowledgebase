# Wald Test
#📥 
%%
#NLP
#concept

**Related:**
-  [[Hypothesis Testing]]

%%

: A [[Hypothesis Testing|hypothesis test]] done of the parameters calculate by the Maximum Liklihood Estimate.
- Checks if the value of the true input parameters has the same likelihood as the parameters calculated by the MLE
- $\theta$: a scalar parameter, a vector of all true input parameters considered under null hypothesis
- $\hat{\theta}$: an estimate of $\theta$, vector of all parameters estimated by the maximum likelihood
- $\hat{se}$ estimated standard error of $\hat{\theta}$

$H_0 : \theta = \theta_0$ VS $H_1 : \theta \ne \theta_0$ 
Assuming $\hat\theta$ is asymptotically normal

Should we move forward with the input parameters or reject them?
- Larger difference between vals -> larger Wald estimate -> reject null hypothesis
- Smaller difference between vals -> larger Wald estimate -> do not reject null hypothesis

Reject $H_0$ when $|W| > z_{a \over 2}$


### From Class
#🔍 *don't follow this*
If you have an estimation of a parameter $\theta$, then assuming $\hat{\theta}$ is asymptotically normal than the null hypothesis $H_0 = \hat{\theta} = \theta_0$ can be rejected if $|W| > Z_{a/2}$ where $W = {\hat{\theta}-\theta_0}/{\hat{se}}$ where $se$ is the standard error 

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

