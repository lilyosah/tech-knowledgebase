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
- $\theta$: a scalar parameter, a vector of all true input parameters considered under null hypothesis (model)
- $\hat{\theta}$: an estimate of $\theta$, vector of all parameters estimated by the maximum likelihood (prediction)
- $\hat{se}$ estimated standard error of $\hat{\theta}$
- $|W|$ is wald test

$H_0 : \theta = \theta_0$ VS $H_1 : \theta \ne \theta_0$ 
Assuming $\hat\theta$ is asymptotically normal
>⭐ **Reject $H_0$ when $|W| > z_{a \over 2}$** (If $|W|$ is outside of the two thingies) 

Should we move forward with the input parameters or reject them?
- Larger difference between vals -> larger Wald estimate -> reject null hypothesis
- Smaller difference between vals -> smaller Wald estimate -> do not reject null hypothesis


### From Class
#🔍 *don't follow this*
If you have an estimation of a parameter $\theta$, then assuming $\hat{\theta}$ is asymptotically normal than the null hypothesis $H_0 = \hat{\theta} = \theta_0$ can be rejected if $|W| > Z_{a/2}$ where $W = {\hat{\theta}-\theta_0}/{\hat{se}}$ where $se$ is the standard error 
Each section is 2.5% so that's why the alpha is divided by 2, the chance that the sample mean ($\hat\theta$) is equal to the population mean ($\theta$)

- Compute $W$
	- $W$ is like an area under part of a s-dev curve... the probability of the thing??? happening?????? 95% chance that they're different 

If you want to test a particular parameter to see if it is different from another, hypothesis 0 is that they are equal, H1 is that they are not

$x = {12, 3, 4}$
$x ~ N(\mu, \sigma)$

**Ex: ✏**  
You have a lot of numbers, just guess that one is the mean, then Wald's test is determining if this is true

#### Applications for NLP
- [[Collocations]]
To tell whether something may be a collocation or not 

Null hypothesis: prob of looking into two words is equal to them being selected independently
- Null: the words appear independently
	- It was not random that two things ended 
- $H_0 : \hat{\theta} = \theta_0$ 

Other prob: If you reject it, you are saying that they are not independent. Knowing one of the words will tell you something about the other one
- Collocation
- $H_1 : \hat{\theta} \ne \theta_0$

$N$ : number of tokens in a corpus 
$P(w_1 w_2) = P(w_1)P(w_2)$
$$\theta_0 = P(w_1)P(w_2)$$
$$\hat\theta = {{c(w_1 w_2)} \over {N}}$$
