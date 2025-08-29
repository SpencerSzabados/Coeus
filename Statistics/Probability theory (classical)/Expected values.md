Expectation of random variables corresponds to the long run average output of a repeated experiment done within the underlying sample space.

# Expectation
The expected value of a random variable is merely its average value, based on its probability distribution. The expected value of a distribution can be thought of as a measure of center.

**Definition: (Expected value)** The _expected value_ of a random variable $g(X)$, is denoted $E(g(X))$, is given by $$E(g(X)) = \begin{cases}\int_{-\infty}^{\infty}g(x)f_X(x)dx &\text{ if $X$ is continuous}\\ \sum_{x\in\mathcal{X}}g(x)f_X(x) = \sum_{x\in\mathcal{X}}g(x)P(X=x) &\text{ if $X$ is discrete,} \end{cases}$$provided that the integral or sum exists.  ^a9ecf6

The expectation of a random variable can also be derived using its cdf opposed to its pdf (or pmf). Namely, if $X$ is a (continuous) random variable with cdf $F_X(x)$ then $$E[X] = \int_{0}^\infty (1-F_X(x))\, dx,$$and more generally for any differentiable function $g$ with $g(0)=0$ $$E[g(X)] = \int_0^\infty(1-F_X(x))\, dg(x).$$This can be seen by recalling $g(t)=\int_0^t g'(x)\, dx$ for such differentiable functions and then $$E[g(X)] = \int_0^\infty g'(x)\int_x^\infty f_X(t)\,dt\,dx = \int_0^\infty g'(x)(1-F_X(x))\, dx$$where $g'(x)dx$ is then combined, [Boris-Belousov](http://boris-belousov.net/2018/01/06/expectation-through-cdf/).

**Lemma: (Linearity of expectation)** The process of taking expectations is a linear operation; that is, for a random variable $X$ and any two constants $a$ and $b$ (or matrices), $E(aX+b)=aE(X)+b.$  ^90ccda

**Theorem:** Let $X$ be a random variable and let $a,b$ and $c$ be constants. Then for any two functions $g_1(x)$ and $g_2(x)$ that have well-defined expectations, 
  1) $E(ag_1(X)+bg_2(X)+c)=aE(g_1(X))+bE(g_2(X))+c$;
  2) If $g_1(x)\geq 0$ for all $x\in \mathcal{X}$, then $E(g_1(X))\geq 0$;
  3) If $g_1(x)\geq g_2(x)$ for all $x\in \mathcal{X}$, then $E(g_1(X))\geq E(g_2(X))$;
  4) If $a\leq g_1(x)\leq b$ for all $x\in \mathcal{X}$, then $a\leq E(g_1(X))\leq b$.

**Observation:** For a random variable $X$, $E[XE[X]]=E[X]E[X]=E[X]^2$. 
This follows from $E[X]$ being constant. This can be generalized easily to two intendent random variables.

**Predictors: (Minimizing distance)** The expected value of a random variable has another property, relating to the interpretation of $E(X)$ as a good "guess" at any assumed value of $X$. Suppose we measure the distance between $X$ and a constant $b$ by $(X-b)^2$. The value of $b$ that minimizes $E[(X-b)^2]$ will serve as a good predictor of $X$. (Note that looking at the value of $b$ that minimizes $(X-b)^2$  does not serve as a good predictor of $X$ as the answer would depend on $X$.) We can derive that $\min_b E[(X-b)^2] = E[(X-E[X])^2]$, and so $b=E[X]$ serves as the best predictor of $X$. 

Expected values can be approximated effectively (depending on sample size etc) by using sample statistics, see [[Random samples]], namely: If $Y=g(X)$ is a random variable, and suppose we are given $N$ observations $x_1,\dots,x_N$ from $\mathcal{X}$, then the expectation of $Y$ can be approximated as $$E[Y] \approx \frac{1}{N}\sum_{i=1}^Ng(x_i).$$This approximation becomes exact as $N\to \infty$, and is know as the [[Random samples#^52b789|sample mean]]. This result can be seen by setting up a [[Maximum likelihood]] problem for the mean of a probability distribution. [[@Bishop_2006]]


## Conditional and joint expectation 
[[Distribution functions of random variables#Conditional distributions and independence|Conditional]] pdfs (or pmfs) can be used to calculate expected values by recalling that $f(y|x)$ is a function of $y$ and calculating pdfs (or pmf) in the same way a before.

**Definition: (Conditional expectation)** If $g(Y)$ is a function of the random variable $Y$, then the _conditional expected value_ of $g(Y)$ for a given $X=x$ is $$E[g(Y)|x] = \begin{cases}\sum_{y}g(y)f(y|x) & \text{if $g(Y)$ is discrete},\\ \int_{-\infty}^\infty g(y)f(y|x)\,dy & \text{if $g(Y)$ is continuous.}\end{cases}$$
Note also that $E[g(Y)|x]$ is a function of $X$ as all values of $Y$ are integrated out; that is, for each value $x$, $E[g(Y)|x]$ is a real number. Thus, $E[g(Y)|x]$ is itself a random variable.

**Lemma: (Law of iterated or total expectation)** Let $X$ and $Y$ be random variables. Then $$E[X] = E[E[X|Y]];$$that is, if $Y$ takes on outcomes $A_1,\dots,A_N$ (meaning these sets form the sample space of $Y$ and therefore form a finite partition of the space from which both $X$ and $Y$ are drawn) then $$E[X] = \sum_{i=1}^N E[X|A_i]P(A_i).$$

It follows from the law of iterated expectation, and the definition of conditional probability, for random variables $X$ and $Y$ we have $$E[X]=E[X|Y]P(Y)+E[X|\overline{Y}]P(\overline{Y}).$$

# Moments and moment generating functions
**Definition: (Moment)** For each integer $n$, the $n$-th _moment_ of $X$ (or $F_X(x)$) is $\mu_n' = E[X^n]$, where $\mu = \mu_1' = E[X]$. The $n$-th _central moment_ of $X$ is $\mu_n = E[(X-\mu)^n]$. ^82311d

**Definition: (Variance)** The _variance_ of a random variable $X$ is its second central moment; that is, $$Var[X] = E[(X-E[X])^2]=E[X^2]-E[X]^2.$$The positive square root of $Var[X]$ is called the _standard deviation_ of $X$. The standard deviation is easier to interpret since the measurement unit is the same as that for the original variable $X$.  ^e635ea

The variance gives a measure of the degree of spread of a distribution around its mean. At the extreme, if $Var[X]=E[(X-E[X])^2]=0$, then $X$ is equal to $E[X]$ with probability $1$, and there is no variation in $X$.

**Theorem:** If $X$ is a random variable with finite variance, then for any constants $a$ and $b$, $Var[aX+b] = a^2Var[X]$. 

**Definition: (Conditional variance)** The variance of the probability distribution $f(y|x)$ is called the _conditional variance_ of $Y$ given $X=x$, and is given by $$Var[Y|x] = E[Y^2|x] - E[Y|x]^2.$$

## Moment generating functions



# Covariance and correlation
Covariance and correlation both measure the strength of the linear relation between random variables.

**Definition: (Covariance)** For two random variables $X$ and $Y$, the _covariance_ of the two is $$Cov[X,Y] = E[(X-E[X])(Y-E[Y])]=E[XY]-E[X]E[Y],$$and expresses the extent to which $X$ and $Y$ vary together. If large values of $X$ are observed in tandem with large values of $Y$, and likewise for small values, then $Cov[X,Y]>0$. If $X$ and $Y$ are independent $Cov[X,Y]=0$. ^d4d0c3

**Definition: (Covariance matrix)** For a random vector $\vec{X} = (X_1,X_2,\dots,X_n)$ the covariance matrix $\Sigma$ is the $n\times n$ matrix with $i,j$ entry equal to $Cov[X_i,X_j]$; $$\Sigma = E[(\vec{X}-E[\vec{X}])(\vec{X}-E[\vec{X}])^\intercal] = \begin{bmatrix} Cov[X_1,X_1] & Cov[X_1,X_2] & \cdots & Cov[X_1,X_n]\\ Cov[X_2,X_1] & \ddots & & \vdots\\ \vdots & & &\\ Cov[X_n,X_1] & \cdots & & Cov[X_n,X_n] \end{bmatrix}.$$
As $\Sigma$ is symmetric and real valued (or complex) its eigenvalues, $\lambda_1,\dots,\lambda_n$, will be real and associated with a set of mutually orthogonal eigenvectors $\vec{u}_1,\dots,\vec{u}_n$. Moreover, the covariance matrix can be decomposed as$$\Sigma = \sum_{i=1}^n \lambda_i\vec{u}_i\vec{u}_i^\intercal\quad \text{ and }\quad \Sigma^{-1} = \sum_{i=1}^n \frac{1}{\lambda_i}\vec{u}_i\vec{u}_i^\intercal.$$ ^962563

Covariances can range in value between $0$ and $\infty$, as such, it is sometimes more convenient to work with correlations which are a normalized measure.

**Definition: (Correlation)** The _correlation_ of $X$ and $Y$ is the number $$\rho_{XY} = \frac{Cov[X,Y]}{\sigma_X\sigma_Y}.$$The correlation constant is bounded $-1\leq \rho_{XY}\leq 1$. With the values $\rho_{XY}=\pm 1$ indicated a perfect _linear_ relationship between $X$ and $Y$. If $X$ and $Y$ are independent then $\rho_{XY}=0$. ^96bfb5

**Definition: (Correlation matrix)** For a random vector $\vec{X} = (X_1,X_2,\dots,X_n)$ the correlation matrix is the $n\times n$ matrix with $i,j$ entry equal to $\rho_{X_i,X_j}$.

Both the covariance and correlation model the linear relationship between the random variables $X$ and $Y$. If the variables do not share a linear relationship, but rather a relationship without a linear component, such as a polynomial relationship, they will have a zero correlation. Thus, if two random variables have correlation zero, it is not guaranteed they are independent. On the other hand, if $X$ and $Y$ are independent then $cov[X,Y]=0$.

**Theorem:** If $X$ and $Y$ are two random variables and $a$ and $b$ are two constants, then $$Var[aX+bY] = a^2Var[X]+b^2Var[Y] + 2abCov[X,Y].$$
**Theorem:** For any random variables $X$ ad $Y$,
   1) $-1\leq \rho_{XY}\leq 1$;
   2) $|\rho_{XY}|=1$ if and only if there exists numbers $a\neq 0$ and $b$ such that $P(Y=aX+b)=1$. If $\rho_{XY}=1$, then $a>0$, and if $\rho_{XY}=-1$, then $a<0$.