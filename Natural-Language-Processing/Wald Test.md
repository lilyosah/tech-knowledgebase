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

