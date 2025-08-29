
# Density projection
We begin by considering the general problem of projecting a density.

Consider a [[Random variables|random variable]] $X:\Omega\to\mathbb{R}^d$ with [[Distribution functions of random variables#^c46bbe|probability density function]] $f$ and let $v\in\mathbb{R}^d$ be a unit vector. Define the random variable $Y=\langle v,X\rangle$ which we want to know the distribution. In order to derive the density, say $f_Y$, of $Y$ let $\phi:\mathbb{R}\to\mathbb{R}$ be any [[Fundamentals of probability theory#^9e67e5|Borel function]] and consider $$E[\phi(Y)]=\int_{\mathbb{R}^d}\phi(y)f_Y(y)\,dy.$$In establishing the form of this expectation we can derive $f_Y$ (TODO - why is this the case?).

Here we have, $$\begin{align*}E[\phi(Y)]=E[\langle v,X\rangle]=\int_{\mathbb{R}^d}\phi(\langle v,x\rangle)f_X(x)\,dx\end{align*}.$$Let $V=span(v)$ and $W=V^{\perp}$ be a [[Orthogonal complement]] of $V$. As such, we can write $\mathbb{R}^d=V\times W$ and every $x\in\mathbb{R}^d$ can be written uniquely as $x=yv+w$ where $y\in\mathbb{R}$ and $w\in W$. Performing this change of variables in the above formulation, and noting that the Jacobina has determinate equal to one since $v$ is a unit vector, gives $$\begin{align*}E[\phi(Y)] &=\int_\mathbb{R}\int_W\phi(v,y v+w)f_X(y v+w)\,dw\,dy\\ &= \int_\mathbb{R}\phi(y)\int_{W}f_X(y v+w)\,dw\,dy\end{align*}$$which implies $$f_Y(y) = \int_{W}f_X(y v+w)\,dw.$$ 

## Gaussian projections 
Unimodal [[Families of distributions#Gaussian (Normal) distribution|Gaussian's]] behave nicely under projection.

Assume $X\sim N(\mu,\Sigma)$ be an $d$-dimensional [[Families of distributions#Gaussian (Normal) distribution|gaussian distribution]] and let $v$ be a unit vector in $\mathbb{R}^d$. Define $Y=v^\intercal X$, and calculate $$E[Y]=E[v^\intercal X]=v^\intercal E[X]=v^\intercal\mu$$and $$Var[Y]=E[(v^\intercal X-v^\intercal\mu)^2]=v^\intercal E[(X-\mu)(X-\mu)^\intercal]v=v^\intercal \Sigma v.$$Thus, we see $Y\sim N(v^\intercal, v^\intercal\Sigma v)$. See [StackExchange-nullgeppetto](https://math.stackexchange.com/questions/1385624/projection-of-gaussian-distribution-along-a-vector).


# Cholesky transformation 
The Cholesky transformation (or Whitening transformation) makes use of the [[Matrix decompositions#Cholesky decomposition|Cholesky decomposition]] applied to the [[Expected values#^962563|covariance matrix]] to [[Statistical transformations|transform]] pairs of random variables which might correlated to following a distribution in which they are uncorrelated; i.e., to map non-isotropic densities to isotropic ones.

**Definition: (Cholesky transformation)** Let $X\sim Uniform(0,I)$, and suppose we wish to generate data, $Y$, according to some distribution $p$ with covariance matrix $\Sigma$ and mean $\mu$. This can be accomplished by letting $Y=\Sigma^{1/2}(X+\mu)$. Likewise, we can perform the oppose transformation using $\Sigma^{-1/2}$. See [itfeature-Ullah](https://itfeature.com/multivariate-statistics/cholesky-transformation). 

It should be noted, there are several different variants of the matrix square root, see [Halvorsen](https://stats.stackexchange.com/a/391633), the Cholesky transformation is the most common when talking about covariances matrices.


# Quantifying a distributions isotropic closeness 
In cases were we want to approximate (estimate) the covariance matrix of a distribution it can be useful to know how different the distribution is from being perfect isotropic (circular), as this can be utilized in forming an upper bound on the quality of our approximation (see [[@Kalai_2006]]).


**Definition: (Isotropic position)** Let $p$ be a distribution over $\mathbb{R}^d$. Then $p$ is said to be in _isotropic position_ if $$E_{v\sim p}[vv^\intercal] = I_d$$

**Definition: (C-isotropic)** A [[Distribution functions of random variables#^c46bbe|density]] $p$ with centroid $\mu$ (mean) is said to be $c$-isotropic if for every unit vector $v\in\mathbb{R}^d$, $$\frac{1}{C}\leq \int_{\mathbb{R}^d} v^\intercal(x-\mu)^2p(x)\,dx\leq C.$$
This provides a measure of how "spherical" a distribution is, where a perfectly spherical distribution with isotropic variance $\sigma^2 I$ would have tight bounds with $C=\sigma^2$; this follows from the fact that $E[(x-\mu)^2]=\sigma^2$ and the above integral being equivalent to taking the expectation of $(x-\mu)^2$ along the vector $v$. ^a2d68c

