The goal of hypothesis testing is to determine, based on sample data, which of two complementary hypotheses is true.

**Definition: (A hypothesis)** A _hypothesis_ is a statement about a population parameter. 

The two complementary hypotheses in a hypothesis testing problem are called the _null hypothesis_ and the _alternative hypothesis_, denoted $H_0$ and $H_1$ repressively. The null hypothesis is used to represent the currently believed result. e.g., a drug has no effect, while the alternative hypotheses is the result you are testing for, e.g., the drug is successful at etc, which is rejected unless sufficient evidence is found that indicates otherwise. The _sufficiency_ of this evidence is some predetermined threshold.

**Hypothesis testing procedure:** A hypothesis test is a rule that specifies: 
  1. For which sample values the decision is made to accept $H_0$ as true;
  2. For which sample values $H_0$ is rejected in favor of $H_1$.
The subset of the sample space for which $H_0$ is rejected is called the _rejection region_ or _critical region_. The complement of this region is called the _acceptance region_.


# Methods of finding tests
There are many methods of testing for statistical results.

## Likelihood ratio tests
The likelihood ratio tests are related to [[Point estimation#Maximum likelihood estimators|maximum likelihood estimators]] and are widely used.

**Definition: (Likelihood ratio test)** If $\vec{X} = (X_1,\dots,X_N)$ is a random sample from a population with pdf (or pmf) $f(\vec{x}|\theta)$, the likelihood function is given as $L(\theta|\vec{x}) = f(\vec{x}|\theta) = \prod_{i=1}^N f(x_i|\theta)$. If $\Theta$ is the parameter space. The _likelihood ratio test statistic_ for testing $H_0:\theta \in \Theta_0\subset \Theta$ versus $H_1:\theta\in \Theta_0^{c}\subset \Theta$ is $$\lambda(\vec{x}) = \frac{\sup_{\Theta_0} L(\theta|\vec{x})}{\sup_\Theta L(\theta|\vec{x})}.$$A _likelihood ratio test_ (LRT) is any test that has a rejection region of the form $\{\vec{x}|\lambda(\vec{X})\leq c\}$, where $c$ is a number satisfying $0\leq c\leq 1$, i.e., the significance of the evidence required to reject $H_0$ in favor of $H_1$.  ^2cca9a

We can approach this in terms of MLEs over a restricted parameter spaces. Suppose $\theta^*$ is an MLE of $\theta$ over the entire parameter space $\Theta$, and $\theta^*_0$ is an MLE over the restricted parameter space $\Theta_0$. Then the LRT statistic can be expressed as $$\lambda(\vec{x}) = \frac{L(\theta^*_0|\vec{x})}{L(\theta^*|\vec{x})}.$$
If $T(\vec{X})$ is a [[Data reduction#^576682|sufficient statistic]] for $\theta$ with pdf (or pmf) $g(t|\theta)$, then we can construct a LRT based on $T$ and its likelihood function $L^*(\theta|t)=g(t|\theta)$ rather than one the sample $\vec{X}$ and its likelihood function $L(\theta|\vec{x})$. In fact the two tests are equivalent.

**Theorem:** If $T(\vec{X})$ is a sufficient statistic for $\theta$ and $\lambda^*(t)$ and $\lambda(\vec{x})$ are the LRT statistics based on $T$ and $\vec{X}$ respectively, then $\lambda^*(T(\vec{x}))=\lambda(\vec{x})$ for every $\vec{x}$ in the sample space.

Likelihood ratio tests (LRT) are useful in situations where _nuisance parameters_ are present, that is, parameters that are present in a model but do not of direct inferential interest. As these parameters can often be replaced by their likelihood estimators in both the numerator and denominator terms of the LRT.


## Bayesian tests
Hypothesis testing problems can be formulated in a [[Bayesian probability theory|bayesian model]], see [[Bayesian hypothesis testing]].


## Union-intersection and intersection-union tests
The _union-intersection method_ of test construction can be useful when the null hypothesis $H_0$ is conveniently expressed as an intersection of the form $$H_0:\theta\in \bigcap_{i\in I}\Theta_i.$$Here $I$ is an arbitrary index set. 

If tests are available (or can be easily constructed) for each of the problems of testing $H_{0,i}:\theta\in\Theta_i$ versus $H_{1,i}:\theta\in \Theta^c_i$; say the rejection region for the tests are $\{\vec{x}\mid T_i(\vec{x})\in R_i\}$. Then the rejection region for the union-intersection test is $$\bigcup_{i\in I}\,\{\vec{x}\mid T(\vec{x})\in R_i\}.$$The rational is, if any one of the hypotheses $H_{0,i}$ are rejected, then $H_0$, which is true only if $H_{o,i}$ is true for all $i\in I$, must also be rejected.

Another method, the _intersection-union method_, is useful if the null hypothesis $H_0$ can be conveniently expressed as a union of the form $$H_0:\theta\in \bigcup_{i\in I}\Theta_i.$$If for each $i\in I$, $\{\vec{x}\mid T_i(\vec{x})\in R_i\}$ is the rejection region for a test of $H_{0,i}:\theta\in \Theta_i$ versus $H_{1,i}:\theta\in \Theta^c_i$, then the rejection region for the intersection-union test of $H_0$ versus $H_1$ is $$\bigcap_{i\in I}\, \{\vec{x}\mid T_i(\vec{x})\in R_i\}.$$Since, $H_0$ is false if and only if all of the $H_{0,i}$ are false, so $H_0$ can be rejected if and only if each of the individual hypotheses can be rejected. 

Both of these tests take on simpler forms if the rejection regions of the individual hypotheses are of the form $\{\vec{x}\mid T_i(\vec{x})\geq c\}$, for some constant $c$ independent of $i$. The rejection regions take on the the following respective forms, $$\bigcup_{i\in I}\,\{\vec{x}\mid T_i(\vec{x})>c\}=\{\vec{x}\mid \sup_{i\in I}T_i(\vec{x})>c\}$$and $$\bigcap_{i\in I}\,\{\vec{x}\mid T_i(\vec{x})\geq c\} = \{\vec{x}\mid \inf_{i\in I}t_i(\vec{x})\geq c\}.$$

# Methods of evaluating tests
Hypothesis tests are typically evaluated and compared through their probabilities of producing incorrect decisions. 

A hypothesis test of $H_0:\theta\in \Theta_0$ versus $H_1:\theta\in \Theta^c_0$ might make one of two types of errors: _Type I Error_ occurs if $H_0:\theta\in \Theta_0$ is incorrectly rejected, a _Type 2 Error_ has occurred if $H_1:\theta\in \Theta_0^c$ is incorrectly rejected in favor of $H_0$.


## Error probabilities and the power function
Suppose $R$ denotes the rejection region for a hypothesis test in question. The probability of Type 1 Error given $\theta\in \Theta_0$ is $P_\theta(\vec{X}\in R)$. For $\theta\in \Theta_0^c$, the probability of Type 2 Error is $P(\vec{X}\in R^c)=1-P_\theta(\vec{X}\in R)$.

**Definition: (Power function)** The _power function_ of a hypothesis test with rejection region $R$ is the function of $\theta$ defined by $\beta(\theta) = P_\theta(\vec{X}\in R)$.

Ideally, the power function is zero valued for all $\theta\in \Theta_0$ and one if $\theta\in \Theta_0^c$. Thus, a good empirical tests have power functions near these values.

The following two terms are useful when discussing tests that control Type 1 Error probabilities. Note that the two terms are sometimes used interchangeably.

**Definition: (Size $\alpha$ test)** For $0\leq \alpha \leq 1$, a test with power function $\beta(\theta)$ with $\sup_{\theta\in \Theta_0} \beta(\theta) = \alpha$ is called a _size $\alpha$ test_.

**Definition: (Level $\alpha$ test)** For $0\leq \alpha \leq 1$, a test with power function $\beta(\theta)$ with $\sup_{\theta\in \Theta_0} \beta(\theta) \leq \alpha$ is called a _level $\alpha$ test_. ^0b0d6d

Experimenters commonly specify the significance level of a hypothesis (LRT) test as one of the following typical values $\alpha\in \{0.01, 0.05, 0.10\}$. Importantly, note by using fixed values we are only controlling Type 1 Error probabilities.

**Notation: (Z-scores and cutoff points)** The notation $z_{\alpha/2}$ is used to denote the point (value) of a standard normal such that $P(Z\geq z_{\alpha/2})=\alpha/2$. The point $z_{\alpha/2}$ itself is known as a cutoff point or critical point. Variants of this notation are used for other distributions.


## p-Values
One common method for reporting the results of a hypothesis test is to report the $\alpha$ size used for the test and the decision of the test. Another way of reporting the results if to report the value of a certain kind of test statistics called a _p-value_.

**Definition: (p-value)** A _p-value_ $\mathit{P}$ is a test statistic satisfying $0\leq \mathit{P}\leq 1$ for every sample point $\vec{x}$. Small value of $\mathit{P}$ give evidence that $H_1$ is true; i.e., smaller p-values indicate stronger evidence for rejecting $H_0$. A p-value is _valid_ if, for every $\theta\in\Theta_0$ and every $0\leq \alpha\leq 1$, $$P_\theta(\mathit{P}\leq \alpha)\leq \alpha.$$Then a test that rejects $H_0$ if and only if $\mathit{P}\leq \alpha$ is a valid level $\alpha$ test. 

An advantage of reporting p-values is that each reader an choose a $\alpha$ they consider appropriate and then can compare the reported $\mathit{P}$ to the chosen $\alpha$ to determine whether these data lead to acceptance of rejection of $H_0$.

The most common way to define (construct) a valid p-value is via the following theorem, or some version of it.

**Theorem:** Let $W(\vec{X})$ be a test statistic such that large values of $W$ give evidence that $H_1$ is true. For each sample point $\vec{x}$, define $$\mathit{P} = \sup_{\theta\in\Theta_0}P_\theta(W(\vec{X})\geq W(\vec{x}))).$$Then, $\mathit{P}$ is a valid p-value.

Another method, which is typically used for discrete data but can also be applied to continuous data, of constructing a p-value is to condition on a sufficient statistic. Namely, suppose $S(\vec{X})$ is a sufficient statistic for the model $\{f(\vec{x}|\theta)\mid \theta\in \Theta_0\}$; to avoid tests with low power it is important that $S$ is sufficient only for the null model. If the null hypothesis is true, the conditional distribution of a random sample $\vec{X}$ given $S=s$ does not depend on $\theta$. Let $W(\vec{X})$ denote a test statistic for which large values give evidence that $H_1$ is true. Then, for each sample $\vec{x}$ define the p-value $$\mathit{P} = P(W(\vec{X})\geq W(\vec{x})|S=S(\vec{x})).$$

## Loss function optimality 
(p400)[[@Casella_2001]]