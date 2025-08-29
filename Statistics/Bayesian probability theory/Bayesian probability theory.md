In short, the Bayesian view states that probabilities provide quantification of uncertainty for the occurrence of an event, opposed to the likelihood any particular event will occur from a series of trials. Bayesian probability can also be used to model events that do not have long run trials are required by frequentist statistics. 

More specifically, per [[@Casella_2001]], in classical statistics a parameter, $\theta$, is thought to be an unknown fixed quantity. A [[Random samples#^fa048e|random smaple]] $X_1,\dots,X_N$ is drawn from a population indexed by $\theta$ and, based on the observed values, knowledge about the values of $\theta$ is obtained. In the Bayesian approach $\theta$ is considered a quantity whose variation can be described by a probability distribution, called the [[Fundamentals of probability theory#^4b7ad7|prior distribution]]. This is a subjective distribution based on the experimenter's belief (judgment), and is formulated before the data is seen (hence the name prior distribution). A sample is then taken from a population indexed by $\theta$ and the prior distribution is updated using [[Fundamentals of probability theory#^4b7ad7|Bayses' rule]] to incorporate the observed sample information. The updated prior distribution is called the [[Fundamentals of probability theory#^4b7ad7|posterior distribution]].    ^abeae7

Although Bayesian statistical methodologies have their origins in the 18th century, the practical applications of Bayesian methods until recently were severely limited by the difficulties in carrying out the required calculations (e.g., marginalizing results such as performing large summations or integration steps over the parameter space). Modern computational methods (e.g., [[Monte Carlo simulation]] and [[Markov chains]] based sampling methods) with the aid of machines elevate much of this.


# Preliminaries 
Much of this is taken from [[@Bishop_2006]], and [[@Gelman_2014]]

Consider (for the remainder) a posterior distribution $$p(\theta|X) \propto p(X|\theta)p(\theta)$$or more accurately $$p(\theta|X)=\frac{p(X|\theta)p(\theta)}{\int p(X|\theta)p(\theta)\,d\theta}$$by including the often intractable marginal denominator $p(X)$.

For the case of forming predictive inferences about the future state of the observable variable $X$ that we have yet to observe we study its [[Distribution functions of random variables#^bfa039|marginal distribution]]; where marginalization refers to summing over all possible values of a chosen variable to  determine the distributional effect of the variable as on the entire joint distribution. 

**Definition: (Prior predictive )** The _prior predictive_ distribution (or also called the [[Bayes likelihood#^f8e946|marginal likelihood]]) $$p(X) = \int p(X,\theta)\, d\theta = \int p(X|\theta)p(\theta)\,d\theta.$$This is called the prior predictive distribution as it is not conditioned on the previous observation of $X$. ^ccc49f

The prior predictive differs form the prior as it output values in the sample space whereas the prior distribution is a distribution over the parameter space. See [Stack-Exchange-periwinkle](https://stats.stackexchange.com/users/231886/periwinkle).

After observing $X$, say we observe the sequence of states $X=(X_1,X_2,\dots,X_N)$, we can form predictions of future values of $X$, assuming the process governing $X$ has not changed, by looking at the _posterior predictive distribution_ which is conditioned on these values (opposed to the prior predictive).

**Definition: (Posterior predictive distribution)** Let $X=(X_1,X_2,\dots,X_N)$ be previously observed values of a random variable $X$, and let $p(X,\theta)$ be the joint distribution (density) of $X$ and a parameter $\theta$, which itself is a random variable, then $$\begin{align}p(\hat{X}|X) &= \int p(\hat{X},\theta|X)\,d\theta\\ &=\int p(\hat{X}|\theta)p(\theta|X)\, d\theta\\ &=\int p(\hat{X}|\theta)\left(\frac{P(X|\theta)p(\theta)}{\int P(X|\theta)p(\theta)\,d\theta}\right)\,d\theta,\end{align}$$which is equal to the average of conditional predictions taken over the posterior distribution of $\theta$.

As the posterior predictive distribution involves an integral over the parameter space exact calculation is often infeasibly expensive (or impossible). Thus, various shortcuts to performing this calculation must typically be used; e.g., it is often easier to calculate a single  value of $\theta$ that maximizes the posterior probability, the [[Maximum posterior]], and plug this in to derive an estimate of $p(\hat{X}|X)$.

## Posterior and averaging of data and prior

Observe (by linearity of expectation) that $$Var[\theta] = E[Var[\theta|X]]+Var[E[\theta|X]],$$from which we can conclude that the posterior variance is on average smaller than the prior variance; i.e., $Var[\theta]\geq E[Var[\theta|X]]$, since variance is always non-negative. See (p32)[[@Gelman_2014]].

We can intuit that the posterior distribution is centered at a point that represents a compromise between the chosen prior and information provided by the observed data, with this compromise being dictated more by the evidence gained from the data than the prior.


## Infeasibility of posterior or marginals
In practice, except for all but a select few classes of distributions, computing the normalizing marginal involved in evaluating a posterior distribution is not feasible (these marginals may not even have closed form solutions). Thus, it is necessary to either formulate problems in different ways or to employ various approximation techniques to various components of these distributions (e.g., approximating the posterior using [[Artificial neural networks]] and indirectly learning the marginal, or [[Monte Carlo simulation]]). 


## Selecting (informative) priors 
Ideally, the chosen prior should include all possible values of $\theta$, recalling that $\theta$ is interpreted as being a random realization of a value from the conditioned prior $p(\theta|\alpha)$ - the distribution need not be centered on the chosen $\theta$ value due to the supporting data shifting the current value, and should follow the same form as the posterior. 

The property that the posterior follows the same (parametric) form as the prior distribution is called _conjugacy_. 

**Definition: (Conjugate prior)** If $\mathcal{F}$ is a class of conditional distributions, say $p(X|\theta)$, and $\mathcal{P}$ is a class of prior distributions of $\theta$, then $\mathcal{P}$ is conjugate for $\mathcal{F}$ if $$p(\theta|X)\in\mathcal{P} \text{ for all } p(X|\theta)\in\mathcal{F} \text{ and }p(\theta)\in \mathcal{P}.$$
Conjugate priors give a closed-form expressions for the posterior probability.

