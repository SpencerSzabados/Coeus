

# Marginal likelihood 
The marginal likelihood ([[Bayesian probability theory|Baye's]] likelihood) of a function is calculated by integrating over the variables that are not of current interest, which _marginalizes them out_ of the expression. The marginal likelihood measures the level of agreement between the observed (supporting) data and the prior distribution.

**Definition: (Marginal likelihood)** Given a iid [[Random samples|random sample]] $X_1,X_2,\dots,X_N$ with $X_i\sim p(x|\theta)$, where $\theta$ is a [[Random variables|random variable]] that parameterizes the sampling distribution $p(x|\theta)$, i.e., $\theta\sim p(\theta|\alpha)$ with $p(\theta|\alpha)$ being the [[Fundamentals of probability theory#^4b7ad7|prior distribution]], the _marginal likelihood_ of observing this sample wrt $\theta$ is $$\mathcal{L}(X_1\dots,X_N|\alpha) = p(X_1,X_2,\dots,X_N|\alpha)=\int_{\theta}p(X_1,\dots,X_N|\theta)p(\theta|\alpha)\,d\theta.$$the marginal likelihood is exactly the normalizing constant of the posterior distribution $$p(\theta|X) = \frac{p(X|\theta)p(\theta)}{\mathcal{L}(X)}$$where the $\alpha$ term is suppresses (as is commonly done) $P(X|\theta)$ is made to be conditioned on $\theta$.  ^f8e946

In general marginal likelihoods are intractable (in practicality) to compute with few having known exact solutions, thus numerical approximation methods are often used (e.g., [[Monte Carlo simulation]]).

The marginal likelihood is very similar in form to the [[Bayesian probability theory#^ccc49f|prior predictive distribution]] when you are in the setting where you are trying to predicted data that is of the same form as your observed samples. The difference being, the marginal likelihood is evaluated over the observed samples and is a scalar valued, where the prior probability is a distribution over the possible values you are predicting (in the sample space); i.e., the marginal likelihood is exactly equal to the prior predictive distribution evaluated at the observed samples.

