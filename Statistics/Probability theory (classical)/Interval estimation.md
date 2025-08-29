Interval estimation, or more general set estimation, is a expanded form of [[Point estimation]] where exact precision of the estimate is reduced in favor of obtaining a probabilistic confidence in capturing the true parameter value being estimated within a interval region. Interval estimates, or more specifically confidence intervals, are commonly used in [[Hypothesis testing]].

**Definition: (Interval estimate)** An _interval estimate_ of a real-valued parameter $\theta$ is any pair of functions, say $L(\vec{x})$ and $U(\vec{x})$, of a sample $\vec{X}$ that satisfies $L(\vec{x})\leq U(\vec{x})$ for all $\vec{x}\in \mathcal{X}$; the random interval $[L(\vec{X}),U(\vec{X})]$ is called an interval estimator. If $\vec{X}=\vec{x}$ is observed, the inference $L(\vec{x})\leq \theta\leq U(\vec{x})$ is made. 

_One-sided interval estimates_ with  $L(\vec{x})=-\infty$ (or $U(\vec{x})=\infty$) can be used for inferencing $\theta\leq U(\vec{x})$ (or $\theta\geq L(\vec{x})$ respectively).  

**Definition: (Coverage probability)** For an interval estimator $[L(\vec{x}),U(\vec{x})]$ of a parameter $\theta$, the _coverage probability_ of $[L(\vec{x}),U(\vec{x})]$ is the probability that the random interval contains the true parameter value, $\theta$; i.e., $P_\theta(\theta\in [L(\vec{X},U(\vec{X}))])=P_\theta(L(\vec{X})\leq \theta, U(\vec{X})\geq \theta)$ or $P(\theta\in [L(\vec{X}),U(\vec{x})]|\theta)$. 

**Definition: (Confidence coefficient)** For an interval estimator $[L(\vec{X}),U(\vec{X})]$ of a parameter $\theta$, the _confidence coefficient_ of $[L(\vec{X}),U(\vec{X})]$ is the infimum of the coverage probabilities, $\inf_{\theta}P_\theta(\theta\in [L(\vec{X}),U(\vec{X})])$. 

Interval estimators together with a measure of confidence (e.g., confidence coefficients) are known as _confidence intervals_, with the terms sometimes being used interchangeably.

The correspondence between acceptance regions of hypothesis tests ([[Hypothesis testing#^0b0d6d|alpha level test]]) and confidence sets (interval) is formalized in the following theorem.

**Theorem:** For each $\theta_0\in\Theta$, let $A(\theta_0)$ be the acceptance region of a level $\alpha$ test of $H_0:\theta=\theta_0$ versus $H_1$ (which dictates the exact form of $A(\theta_0)$ so is left unspecified). For each $\vec{x}\in\mathcal{X}$, define a set $C(\vec{x})\subset \Theta$ by $$C(\vec{x})=\{\theta_0:\vec{x}\in A(\theta_0)\}.$$Then the random set $C(\vec{X})$ is a $1-\alpha$ confidence set; note that, $C(\vec{x})$ may not be an interval for any $A(\theta_0)$. Conversely, let $C(\vec{X})$ be a $1-\alpha$ confidence set, and for any $\theta_0\in\Theta$, define $$A(\theta_0)=\{\vec{x}:\theta_0\in C(\vec{x})\}.$$Then $A(\theta_0)$ is the acceptance region of a level $\alpha$ test of $H_0$.


# Methods for constructing interval estimators

## Inverting a test statistic 
The most powerful [[Hypothesis testing#^0b0d6d|fixed alpha level test]], and most common, type of interval test for normally distributed data is the following.

**Example: (Normal Z-score interval test)** Let $\vec{X}=(X_1,\dots,X_N)$ be idd $\mathcal{N}(\mu,\sigma^2)$ and consider the hypothesizes test of $H_0:\mu=\mu_0$ versus $H_1:\mu\neq \mu_0$. For a fixed $\alpha$ level we want to utilize the rejection region $\{\vec{x}: |\overline{x}-\mu_0|>z_{\alpha/2}\sigma/\sqrt{n}\}$, so $P(H_0\text{ is rejected }|\mu=\mu_0)=\alpha$ or vice versa $P(H_0\text{ is accepted }|\mu=\mu_0)=1-\alpha$. As these statements holds for all values of $\mu_0$ so we get $$P\left(\overline{X}-z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\leq \mu\leq\overline{X}+z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right)=1-\alpha,$$  
and the corresponding $\alpha$ level test interval of $[\overline{x}-z_{\alpha/2}\sigma/\sqrt{n},\overline{x}+z_{\alpha/2}\sigma/\sqrt{n}]$. (p421)[[@Casella_2001]]


## Pivotal quantities
**Definition: (pivotal quantity)** A random variable $Q(\vec{X},\theta)$ is a _pivotal quantity_ if the distribution of $Q(\vec{X},\theta)$ is independent of all parameters. That is, if $\vec{X}\sim F(\vec{x}|\theta)$, then $Q(\vec{X},\theta)$ has the same distribution for all values of $\theta$.

The method of constructing confidence sets from pivots relies on being able to find a pivot and a set $A$ such that $\{\theta\mid Q(\vec{x},\theta)\in A\}$ is a set estimate of $\theta$. 

Once we have a pivot, $Q(\vec{X},\theta)$, the for a specified value of $\alpha$ we can find constants $a\leq b$ such that $$P_\theta(a\leq Q(\vec{X},\theta)\leq b)\geq 1-\alpha.$$Then for each $\theta_0\in\Theta$, we get the acceptance region$$A(\theta_0) = \{\vec{x}\mid a\leq Q(\vec{x},\theta_0)\leq b\}$$for a level $\alpha$ test of $H_0:\theta=\theta_0$. 

From this we can construct a confidence set, using the pivot to specify the specific form of the acceptance region, we obtain $$C(\vec{x}) = \{\theta_0\mid a\leq Q(\vec{x},\theta_0)\leq b\},$$which is a $1-\alpha$ confidence set for $\theta$. If $\theta$ is a real valued parameter and if, for each $\vec{x}\in\mathcal{X}$, $Q(\vec{x},\theta)$ is a monotone function in $\theta$, the $C(\vec{x})$ will be an interval. Moreover, if $Q(\vec{x}.\theta)$ is an increasing function of $\theta$, then $C(\vec{x})$ can be expressed in the form $L(\vec{x},a)\leq \theta\leq U(\vec{x},b)$. Likewise, if $Q(\vec{x}.\theta)$ is a decreasing function of $\theta$, then $C(\vec{x})$ can be expressed in the form $L(\vec{x},b)\leq \theta\leq U(\vec{x},a)$.

**Example: (Normal pivotal interval)** If $\vec{X}=(X_1,\dots,X_N)$ are iid $\mathcal{N}(\mu,\sigma^2)$, then $(\overline{X}-\mu)/(\sigma/\sqrt{n})$ is a pivot. If $\sigma^2$ is known, this pivot can be directly used to calculate the confidence interval for $\mu$. For any constant $a>0$, $$P\left(-a\leq \frac{\overline{X}-\mu}{\sigma/\sqrt{n}}\leq a\right)=P(-a\leq Z\leq a), \quad\text{($Z$ is standard normal)}$$and we get the confidence interval $$\{\mu\mid \overline{x}-a\sigma/\sqrt{n}\leq \mu\leq\overline{x}+a\sigma/\sqrt{n}\}$$. If $\sigma^2$ is not known, we can use the location-scale pivot (student's t distribution) $(\overline{X}-\mu)/(S/\sqrt{n})$, where $$P\left(-a\leq\frac{\overline{X}-\mu}{S/\sqrt{n}}\leq a\right)=P(-a\leq T_{n-1}\leq a).$$Thus, for any $\alpha$, if we take $\alpha=t_{n-1,\alpha/2}$, we get a $1-\alpha$confidence internal $$\{\mu\mid \overline{x}-t_{n-1,\alpha/2}s/\sqrt{n}\leq \mu\leq \overline{x}+t_{n-1,\alpha/2}s/\sqrt{n}\}.$$

### Pivoting the CDF
Here we will work with a more general pivot than above, with under minor assumptions, will guarantee an interval form confidence set. In most situations inverting an LRT, is possible, is recommended as the resulting set may not be optimal but will never be very bad. However, in some cases this is not feasible.

We will construct confidence intervals for a parameter $\theta$ on a real-valued statistic $T$ with cdf $F_T(t|\theta)$; it is usually taken that $T$ is a sufficient statistic but this is not necessary for the following theorem. 
p(431)[[@Casella_2001]]




