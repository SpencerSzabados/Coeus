A distribution family is indexed by one or more parameters, which allow us to vary certain characteristics of the distribution without changing the underlying equations. Distribution parameters are often emphasized by being written in the associated pmf (or cdf, pdfs, expectations, etc) preceded by a "|".


# Discrete distributions 
### Discrete uniform distribution
A random variable $X$ has a _discrete uniform_ $(1,N)$ _distribution_ if $$P(X=x|N) = \frac{1}{N} \text{ , } x=1,2\dots,N,$$where $N$ is a preselected integer. Here, $E[X] = (N+1)/2$ and $Var[X] = (N+1)(N-1)/12$. This distribution can be easily generalized to a range of integers between $N_0$ and $N_1$, with pmf $P(X=x|N_0,N_1)=1/(N_1-N_0+1)$. 


## Bernoulli distribution 
A Bernoulli trial is an experiment that results in one of two possible outcomes, typically $\{0,1\}$, with a set probability $p$. 

A random variable $X$, with range $\mathcal{X}=\{0,1\}$, has _$Bernoulli(p)$ distribution_ if $$X = \begin{cases}1 & \text{ with probability }p\\ 0 & \text{ with probability }1-p, \end{cases}\quad 0\leq p\leq 1.$$Equivalently, the probability of seeing any particular observation $X=x$ can written as $$P(X=x|p) = p^x(1-p)^{1-x}$$for a discrete random variable $X$ with Bernoulli distribution.

The mean and variance of a $Bernoulli(p)$ random variable $X$ are: $E[X] = p$, and $Var[X]=p(1-p)$. 

#### Examples 
  + https://stats.stackexchange.com/questions/294737/what-is-the-variance-of-a-binomial-distribution-with-1-and-1


## Binomial distribution
The binomial distribution generalizes the Bernoulli distribution, by counting successes occurring within a sequence of of Bernoulli trials.

If $n$ identical Bernoulli trials are performed, define the events $$A_i = \{X=1 \text{ on the $i$-th trial}\},\quad i=1,2\dots,n.$$Assuming the events to be independent, we can derive the distribution of the total number of success in $n$ trials. Define a random variable $Y$ to equal the total number of success in $n$ trials. The event $\{Y=y\}$ will occur if exactly $y$ of the events $A_1,A_2,\dots,A_n$ succeed (occur). There exists $n\choose y$ possible orders of $y$ successful events from the given set of $n$ events. Let $A_1\cap A_2\cap A_3^c\cap \cdots \cap A_{n-1}\cap A_n^c$ be one particular such ordering. This has probability of occurrence $P(A_1\cap A_2\cap A_3^c\cap \cdots \cap A_{n-1}\cap A_n^c) = p^y(1-p)^{n-y}$.  Then a particular sequence of $n$ trials with exactly $y$ successes occurs with probability $$P(Y=y|n,p) = {n\choose y}p^y(1-p)^{n-y}, \quad y=0,1,2\dots, n.$$The random variable $Y$ is called a $Binomial(n,p)$ _random variable_. 

The mean and variance of the binomial distribution are: $E[X] = np$ and $Var[X] = np(1-p)$.


## Multinomial distribution 
A convenient representation for a discrete [[Random variables|random variable]] $X$ with $k$ possible values is a $k$-dimensional random vector of the form $\vec{X} = (X_1,X_2,\dots,X_K)$, where at most one entry is allowed to be non-zero at any given moment. The non-zero value indicates which of the $k$ possible values is realized by $X$; if the $i$ possible value is observed then $X_i=1$, and $X_j=0$ for all $j\neq i$. 

Under this representation, we have by construction $$\sum_{i=1}^k X_i = 1.$$If for each component $0\leq P(X_i=1)=p_i\leq 1$ with $\vec{p}=(p_1,p_2,\dots,p_k)$ such that $\sum_{i=1}^k p_i = 1$, then $$P(\vec{X}=\vec{x}|\vec{p}) = \prod_{i=1}^k p_i^{x_i}.$$Moreover, this probability is properly normalized since $\sum_{\vec{x}\in \{0,1\}^k} P(\vec{X}=\vec{x}|\vec{p}) = \sum_{i=1}^k p_k =1$. With [[Expected values|expectation]]  $$E[\vec{X}|\vec{p}] = \sum_{\vec{x}} \vec{x}P(\vec{X}=\vec{x}|\vec{p}) = \vec{p}.$$
The multinomial distribution gives a distribution for the number of observations of a specific value from a multinomial random variable, much like the binomial distribution and Bernoulli random variables.

Given a set of observations $\vec{x_1},\dots,\vec{x_N}$ of $\vec{X}$. The corresponding likelihood function is given as $$P(m_1,m_2,\dots,m_k|\vec{p}) = \prod_{i=1}^k p_i^{m_i}$$where $m_i$ is the number of observations with $i$-th component equal to one and obeys the constraint $\sum_{i=1}^k m_i = N$. The multinomial distribution is then given by $$\begin{align} Multi(m_1,m_2,\dots,m_k|\vec{p},N) &= \binom{N}{m_1m_2\dots m_k}\prod_{i=1}^k p_i^{m_k}\\ &= N!\prod_{i=1}^k\frac{p_i^{m_i}}{m_i!}.\end{align}$$
Or to state this in terms of random variables that count the number of observations, we have

**Definition: (Multinomial distribution)** Let $(X_1,X_2,\dots,X_k)$ be a random vector where $X_i$ counts the number of times value $1\leq i\leq k$ is realized within $N$ trials, with probabilities $p_1,p_2,\dots,p_k$ respectively. Then the joint pmf of $(X_1,\dots,X_k)$ is given by the _multinomial distribution_ of $N$ trials, $$Multi(x_1,x_2,\dots,x_k|\vec{p},N) = \binom{N}{x_1x_2\dots x_k}\prod_{i=1}^k p_i^{x_k}.$$
We can see by calculating the marginal distributions of each component (or a collection of components) that each has a binomial distribution; particularly, $X_i\sim \mathcal{N}(N,p_i)$.

The coordinates of the vector $(X_1,\dots,X_k)$ are negatively correlated, with $$Cov[X_i,X_j] = E[(X_i-p_i)(X_j-p_j)] = -Np_ip_j.$$This can be reconciled by noting the total is constrained by $N$, so if one element takes up a large portion the others must tend not to.

# Continuous distributions 
## Gaussian (Normal) distribution 
The normal distribution and distribution associated with play large roles in statistics for a number of reasons. Firstly, gaussian distributions are very analytically tractable (especially compared to some others). Secondly, the distribution is symmetric across a vertical line of symmetry (when not skewed) which makes it an appealing choice for population models. Third, there is the [[Random samples|Central limit theorem]], which shows, under mild conditions, the normal distribution can be used to approximate a large variety of distributions.

**Definition: (Normal distribution)** The pdf of a _normal distribution_ with mean $\mu$ (expectation) and variance $\sigma^2$, usually denoted by $\mathcal{N}(\mu,\sigma^2)$, is given by $$f(x|\mu,\sigma^2) = \frac{1}{\sqrt{2\pi}\sigma}e^{-(x-\mu)^2/2\sigma^2},\quad -\infty<x<\infty.$$This quantity is sometimes also expressed, in a minor abuse of notation, as $\mathcal{N}(x|\mu,\sigma^2)$.

**Definition: (Standard normal distribution)** If $X\sim \mathcal{N}(\mu,\sigma^2)$, then the random variable $Z=(X-\mu)/\sigma$ has $\mathcal{N}(0,1)$ distribution, and is known as the _standard normal distribution_. This can be explicitly seen by calculating $$\begin{align} P(Z\leq z) &= P\left(\frac{X-\mu}{\sigma}\leq z\right)\\ &= P(X\leq z\sigma+\mu)\\ &= \frac{1}{\sqrt{2\pi}\sigma}\int_{-\infty}^{z\sigma+\mu} e^{-(x-\,u)^2/s\sigma^2}\,dx\\ &=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{z}e^{-t^2/2}\,dt, \quad \left(\text{subsitute } t=\frac{x-\mu}{\sigma}\right).\end{align}$$which shows $P(Z\leq z)$ is the standard normal cdf. We can further calculate $$E[Z] = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^\infty ze^{-z^2/2}\,dz = -\frac{1}{\sqrt{2\pi}}e^{-x^2/2}\bigg|_{-\infty}^\infty = 0,$$ to show this.

[[Statistical inequalities and identities#^3a15e0|Stein's Lemma]] makes it easy to calculate higher-order moments of a normal distribution. If $X\sim \mathcal{N}(\theta,\sigma^2)$, then for example, $$\begin{align} E[X^3] &= E[X^2(X-\theta+\theta)]\\ &= E[X^2(X-\theta)]+\theta E[X^2]\\ &=2\sigma^2E[X]+\theta E[X^2]\\ &=3\theta\sigma^2+\theta^3. \end{align}$$

### Approximating the binomial distribution using normal distribution 
If $X\sim bionmial(n,p)$, then $E[X]=np$ and $Var[X]=np(1-p)$, and under _suitable conditions_, the distribution of $X$ can be approximated by a normal random variable with mean $\mu=np$ and variance $\sigma^2=np(1-p)$. The aforementioned "suitable conditions" are that $n$ should be large enough (discrete) as to resemble a normal distribution (many intermediate values) and $p$ should not be far removed from $0.5$. A conservative rule of thumb to follows is to require $min\{np,np(1-p)\}\geq 5$. 
 
See [[Density estimation#Parameter estimation]] for how to fit parameters for the normal distribution and a more detailed view of parametric distribution fitting.


### Bivariate normal distribution
**Definition: (Bivariate normal distribution)** Given two random variables $X$ and $Y$ with means $\mu_X$, $\mu_Y$, variances $\sigma_X$, $\sigma_Y$, and [[Expected values#^96bfb5|correlation constant]] $\rho$, the bivariate pdf of $X$ and $Y$ is given by $$f(x,y) = \left(2\pi\sigma_X\sigma_Y\sqrt{1-\rho^2}\right)^{-1}\cdot exp\left(-\frac{1}{2(1-\rho^2)}\left[\left(\frac{x-\mu_X}{\sigma_X}^2\right)-2\rho\left(\frac{x-\mu_X}{\sigma_X}\right)\left(\frac{y-\mu_Y}{\sigma_Y}\right)+\left(\frac{y-\mu_Y}{\sigma_Y}\right)^2\right]\right),$$for $x,y\in \mathbb{R}$.  The marginal distributions of $X$ and $Y$ are each normal distributions; particularly, $$f_X(x) = \frac{1}{\sqrt{2\pi}\sigma_X}e^{-(x-\mu_X)^2/2\sigma_X^2}\quad \text{and}\quad f_Y(y) = \frac{1}{\sqrt{2\pi}\sigma_Y}e^{-(y-\mu_Y)^2/2\sigma_Y^2},$$ as expected. Moreover, we have the joint expectation (or second moment) $$\begin{align} E[XY] &=E[E[XY|Y]] = E[YE[X|Y]]&& \text{(Iterated rule of conditional expectation)}\\ &=E[Y(\mu_X+\rho\sigma_X/\sigma_Y(Y-\mu_Y))]\\ &=\mu_XE[Y] + \rho\sigma_X/\sigma_Y(E[Y^2]-\mu_YE[Y])\\ &=\mu_X\mu_Y+\rho\sigma_X\sigma_y.\end{align}$$

### Higher dimensions
**Definition: (higher dimensions)** If $\vec{X}=(X_1,X_2,\dots,X_n)$ is a $n$-dimensional random vector of continuous variables, the normal distribution of $\vec{X}$ is given as $$f(\vec{x}|\vec\mu,\Sigma) = \frac{1}{(2\pi)^{d/2}\det(\Sigma)^{1/2}}\exp\left(-\frac{1}{2}(\vec{x}-\vec{\mu})^\intercal\Sigma^{-1}(\vec{x}-\vec{\mu})\right)$$where $\Sigma$ is the $n\times n$ [[Expected values#^962563|covariance matrix]] of $\vec{X}$.

The high dimensional normal distribution has expectation $E[\vec{X}] = \vec{\mu}$ and second moment  $E[\vec{X}\vec{X}^\intercal] = \vec{\mu}\vec{\mu}^\intercal + \Sigma$.


## Chi-squared distribution 

**Definition: (Chi-squared distribution)** A random variable $X$ (or vector for $k>1$) with [[Distribution functions of random variables#^c46bbe|probability density function]] of the form $$f(x,k) = \begin{cases}\frac{x^{k/2-1}e^{-x/2}}{s^{k/2)\Gamma(k/2)}} &\text{ if }x>0\\ 0 &\text{ otherwise} \end{cases}$$is said to follow a chi-squared distribution with $k$-degrees of freedom, where $\Gamma$ is the gamma function.

**Lemma:** Let $\chi_p^2$ be a chi-squared random variable with 
$p$ degrees of freedom. Then ^70a18f
   1) If $Z$ is a $\mathcal{N}(0,1)$ random variable, then $Z^2\sim \chi_1^2$; that is, the square of a standard normal random variable is a chi-squared random variable.
   2) If $X_1,\dots,X_N$ are independent and $X_i\sim \chi_{p_1}^2$, then $X_1+\cdots +X_N\sim \chi_{p_1+\cdots+p_N}^2$; that is, independent chi-squared variables add to a chi-squared variable, and the degrees of freedom also sum.


## Beta distribution 
^2818d2
The beta distribution is one of the few commonly used distributions that give probability 1 to a finite interval, namely $(0,1)$, and as a consequence if often used to model proportions.

The Beta family of distributions is a continuous family on $(0,1)$ indexed by two parameters. The $Beta(\alpha,\beta)$ pdf is $$f(x|\alpha,\beta) = \frac{1}{B(\alpha,\beta)}x^{\alpha-1}(1-x)^{\beta-1},\quad 0<x<1,\,\alpha>0,\,\beta>0,$$where $B(\alpha,\beta)$ denotes the beta function, which serves as a normalization constant, and is given by $$B(\alpha,\beta) = \int_0^1x^{\alpha-1}(1-x)^{\beta-1}\,dx = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)},$$and $\Gamma$ is the gamma function. 

The mean and variance are respectively $E[X] = \alpha/(\alpha+\beta)$ and $Var[X] = \alpha\beta / (\alpha+\beta)^2(\alpha+\beta+1)$.


## Dirichlet distribution 
# Exponential family of distributions

**Definition (Exponential family):** A family of pdfs or pmfs is called an _exponential family_ if it can be expressed in the from $$f(x|\theta) = h(x)c(\vec\theta)\exp\left(\sum_{i=1}^k w_i(\vec\theta)t_i(x)\right),$$where $h(x)\geq 0$, $t_1(x),\dots,t_k(x)$ are real-valued functions of the observation $x$ independent of $\vec\theta$,  $c(\vec\theta)\geq 0$, and $w_1(\vec\theta),\dots,w_k(\vec\theta)$ are real valued functions of the possibly vector-valued parameter $\vec\theta$ which are likewise independent of $x$. 

Alternatively, we can write $$f(x|\theta) = \exp\left(\theta^\intercal T(x)-A(\theta)+B(x)\right)$$where $\theta$ is a vector of parameter values, $T$ is a sufficient statistic for $x$ (this is the same as above), $A$ is a normalizing function dependent on $\theta$ and independent of $x$, and $B$ is an arbitrary function. [ref: cs680 lecture].

Many common continuous families belong to the exponential class of families, e.g., Normal, Gamma, Beta, and the discretized Binomial and Poisson. 