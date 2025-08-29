# Cumulative probability
The cumulative probability of a random variable (event) is a fundamental concept.

**Definition: (Cumulative distribution function)** The _cumulative distribution function_ or _cdf_ of a random variable $X$, denoted $F_X(x)$, is defined as $$F_X(x) = P_X(X\leq x), $$for all $x$. Observe that cdf of a function is defined for all real valued inputs not just those within $\mathcal{X}$; however, it might not be continuous, with the size of a jump at any point $x$ equaling $P(X=x)$. Thus, whether or not a cdf is continuous is dependent on the continuity of the underlying random variable. ^1a548c

**Theorem:** The function $F(x)$ is a cdf if and only if the following three conditions are satisfied: 
  1) $\lim_{x\to -\infty} F(x) = 0$ and $\lim_{x\to \infty} F(x) = 1$;
  2) $F(x)$ is a nondecreasing function in terms of $x$;
  3) $F(x)$ is right-continuous; that is, for every number $x_0$, $\lim_{x\to x_0^{+}}F(x)=F(x_0)$;
  4) For al $a<b$ (within the range of $X$), $P(a<X<b)=P(X\leq b)-P(X\leq a)=F(b)-F(a)$; 

Note, some authors make it a requirement that the cdf be a monotonically increasing function rather than only nondecreasing (along with corresponding changes to other properties). 

**Definition: (Identically distributed)** Two random variables $X$ and $Y$ are _identically distributed_ if for every set $A\in \mathcal{B}$,  taken from the _Borel field_ $\mathcal{B}$ associated with the sample space $S$, $P(X\in A)=P(Y\in A)$. Equivalently, in terms of cdfs this becomes $F_X(x)=F_Y(x)$ for every $x$. 

The common expression "$X$ has a distribution given by $F_X(x)$" is abbreviated symbolically to "$X\sim F_X(x)$". Likewise, if two random variables $X$ and $Y$ have the same distribution, we write $X\sim Y$.


# Density and mass functions
Associated to each random variable $X$ and its cdf $F_X$ is another function, called the _probability density function (pdf)_ or _probability mass function (pmf)_, respectively used when $X$ is continuous or discontinuous.

**Definition: (Probability mass function)** The _probability mass function (pmf)_ of a discrete random variable $X$ is given by $f_X(x)=P(X=x)$ for all $x$; that is, the pointwise probabilities of a discrete random variable is equivalent to the value of its pmf at that point.

**Definition: (Probability density function)** The _probability density function (pdf)_ of a continuous random variable $X$ is the function $f_x$ that satisfies: $F_X(x) = \int_{-\infty}^x f_X(t)dt$ for all $x$. Unlike for discrete random variables, in the continuous case $P(X=x)=0$ for any singular observation $x$ by definition of the cdf, and therefore $P(a<X<b) = P(a\leq X\leq b)$. ^c46bbe

Unlike for pmfs, pointwise values of pdfs do not represent probabilities (breaks definition of probability) but rather a pointwise weight of an individual values occurrence relative to that of others. Thus, one must be careful to not confuse pdf and pmf, and more generally to not mistakenly refer to pdf as probabilities and attempt to manipulate them as such without thought.

**Theorem:** A function $f_X(x)$ is a pdf (or pmf) of a random variable $X$ if and only if the following two properties hold:
  1) $f_X(x)\geq 0$ for all $x$;
  2) $\sum_{x}f_X(x)=1$ for pmfs or $\int_{-\infty}^\infty f_X(x)dx=1$ in the case of pdfs. 


## Joint distributions 
Typical experiments observe the values of multiple [[Random variables]]. Thus, we need to know how to deal with probability models that describe the behaviors of more than one random variable. 
^fa2cbe

### Discrete distributions
**Definition: (Discrete join distribution)** Let $(X,Y)$ be a discrete random vector. Then the function $f(x,y):\mathbb{R}^2\to \mathbb{R}$ defined by $f(x,y)=P(X=x,Y=y)$ is called the _joint probability mass function_ or _joint pmf_ of $(X,Y)$.

Let $A\subset \mathbb{R}^2$. Then $P((X,Y)\in A) = \sum_{(x,y)\in A} f(x,y)$.

Let $g(X,Y)$ be a real-valued function defined for all possible values $(x,y)$ of the discrete random vector $(X,Y)$. Then $g(X,Y)$ is itself a random variable, see [[Statistical transformations]], with [[Expected values#^a9ecf6|expectation]] $$E[g(X,Y)] = \sum_{(x,y)\in \mathbb{R}^2} g(x,y)f(x,y).$$
There are situations where we may wish to study the distribution of a single component of a random vector rather than deal with the distribution of the entire vector. These are the so called _marginal distributions_ of a random vector. The marginal distribution of a random vector are completely determined by the distribution of the entire vector, as can be seen by the following theorem.

**Theorem: (Marginal pmfs)** Let $(X,Y)$ be a discrete random vector with joint pmf $f_{X,Y}$. Then the _marginal pmfs_ of $X$ and $Y$, $f_X(x)=P(X=x)$ and $f_Y(y)=P(Y=y)$ respectively, are given by $$f_X(x) = \sum_{y\in\mathbb{R}}f_{X,Y}(x,y) \quad\text{and}\quad f_Y(y) = \sum_{x\in\mathbb{R}}f_{X,Y}(x,y).$$
Thus, the marginal distributions of a random vector can be seen as the projection of the joint distribution onto a coordinate axis. [Encyclopedia of Mathematics](http://encyclopediaofmath.org/index.php?title=Marginal_distribution&oldid=47762).

While the marginals are specified by the joint pmf we cannot, in general, re-construct the joint pmf of $(X,Y)$ given only the univariant pmfs of $X$ and $Y$ without additional information; i.e., we require the [[Expected values#Covariance and correlation|covariance]] information, e.g., if we know $X$ and $Y$ are independent then the joint pmf (or pdf) can be found to be $f_X(x)f_Y(y)$.


### Continuous distributions
**Definition: (Continuous joint distribution)** A function $f:\mathbb{R}^2\to \mathbb{R}$ is called a _joint probability density function_ or _joint pdf_ of the continuous bivariate random vector $(X,Y)$ if, for every $A\subseteq \mathbb{R}^2$, $$P((X,Y)\in A) = \int\int_A f(x,y)\,dA.$$
It is worth noting that the joint pdf is defined for all points in $\mathbb{R}^2$, but may equal zero on a large set. Indeed, it is commonly assumed, unless otherwise mentioned, that arguments not assigned probabilities explicitly have probability zero.

If $g(x,y)$ is a real-valued function, then the expected value of $g(X,Y)$ is defined to be $$E[g(X,Y)] = \int_{-\infty}^\infty\int_{-\infty}^\infty g(x,y)f(x,y)\,dx\,dy,$$similar to the univariant case.

**Theorem: (Marginal pdfs)** The _marginal probability density functions_ of $X$ and $Y$ are defined as $$\begin{align} f_X(x) &= \int_{-\infty}^\infty f(x,y)\,dy\quad \text{for $-\infty<x<\infty$},\\ f_Y(y) &= \int_{-\infty}^\infty f(x,y)\,dx\quad \text{for $-\infty<y<\infty.$}\end{align}$$
The joint probability distribution of $(X,Y)$ can be completely described with the _joint cdf_.  ^bfa039

**Definition: (Joint cdf)** Given a random vector $(X,Y)$. The joint cdf is the function $F(x,y)$ defined by $$\begin{align*}F(x,y) &= P(X\leq x,Y\leq y)\\ &= \int_{-\infty}^x\int_{-\infty}^y f_{X,Y}(u,v)\,du\,dv.\end{align*}$$ for all $(x,y)\in \mathbb{R}^2$. The bivariate Fundamental theorem of calculus gives $$\frac{\partial^2 F(x,y)}{\partial x\partial y} = \frac{\partial^2 F(x,y)}{\partial y\partial x}= f(x,y)$$within continuous regions of $f(x,y)$. Similarly for the discrete case, with substitution of the integrals by summations. ^89539c


### Conditional distributions and independence
If $(X,Y)$ is a discrete random vector, the a conditional probability of the from $P(X=x|Y=y)$ is interpreted exactly like that in [[Fundamentals of probability theory#Conditional probability and independence]]. Likewise, the same rules governing basic conditional probabilities apply here. These ideas are not formalized in terms of random vectors.

**Definition: (Discrete conditional distribution)** Let $(X,Y)$ be a discrete bivariate random vector with joint pmf $f(x,y)$ and marginal pmfs $f_X(x)$ and $f_Y(y)$. For any $x$ such that $P(X=x)=f_X(x)>0$, the conditional pmf of $Y$ for fixed $X=x$ is the function of $y$ defined by $$f(y|x) = P(Y=y|X=x) = \frac{f(x,y)}{f_X(x)}.$$On the other hand, for any $y$ such that $P(Y=y)>0$, the conditional pmf of $X$ for $Y=y$ is given as $$f(x|y) = P(X=x|Y=y) = \frac{f(x,y)}{f_Y(y)}.$$
If $X$ and $Y$ are continuous random variables, $P(X=x)=0$ for any singular value. With that said, $f_X(x)$ has nonzero value whenever $x$ lies on the support of $X$, and so we can define the conditional probabilities for continuous random variables analogously to those above. 

**Definition: (Continuous conditional distribution)** Let $(X,Y)$ be a continuous bivariate random vector with joint pdf $f(x,y)$ and marginal pdfs $f_X(x)$ and $f_Y(y)$. Then for any $x$ such that $f_X(x)>0$, the conditional pdf of $Y$ given $X=x$ is the function $$f(y|x) = \frac{f(x,y)}{f_X(x)}.$$Likewise, for any $y$ with $f_Y(y)>0$, the conditional pdf of $X$ given $Y=y$ is given by $$f(x|y) = \frac{f(x,y)}{f_Y(y)}.$$

**Definition: (Random variable independence)** Let $(X,Y)$ be a random vector with joint pdf (or pmf) $f(x,y)$. Then $X$ and $Y$ are _independent random vectors_ if and only if there exists functions $g(x$) and $h(y)$ such that, for every $x,y\in \mathbb{R}$, $$f(x,y) = g(x)h(y).$$The choices of $g(x)=f_X(x)$ and $h(y)=f_Y(y)$ are sufficient, but can be harder to compute than other choices. This is an identical notion of independence as that for primitive events, see [[Fundamentals of probability theory#^a6f427|statistical independence]]. ^0257fe

We can characterize the independence of random variables by looking at their supports: If $X$ and $Y$ are independent random variables, then $f(x,y)>0$ on the set $A\times B = \{(x,y)\mid x\in A,\,y\in B\}$ where $A=\{x\mid f_X(x)>0\}$ and $B=\{y\mid f_Y(y)>0\}$. On the other hand, if $f(x,y)>0$ on a set that is not of cross-product form, then the random variables $X$ and $Y$ are not independent.

**Theorem:** Let $X$ and $Y$ be independent random variables. Then
   1) For any $A\subset \mathbb{R}$ and $B\subset \mathbb{R}$, $P(X\in A, Y\in B) = P(X\in A)P(Y\in B)$; that is, the events $\{X\in A\}$ and $\{Y\in B\}$ are independent.
   2) Let $g(x)$ be a function only of $x$ and $h(y)$ be a function only of $y$. Then $$\begin{align} E[g(X)h(Y)]&=\int_{-\infty}^\infty\int_{-\infty}^\infty g(x)h(y)f(x,y)\,dx\,dy\\ &=\int_{-\infty}^\infty\int_{-\infty}^\infty g(x)h(y)f_X(x)f_Y(y)\,dx\,dy\\ &=\int_{-\infty}^\infty g(x)f_X(x)\,dx\int_{-\infty}^\infty h(y)f_Y(y)\,dy\\ &= E[g(x)]E[h(y)].\end{align}$$Result (2) holds likewise in the discrete case.

**Property: (Sum of independent variables)** let $X\sim \mathcal{N}(\mu,\sigma^2)$ and $Y\sim \mathcal{N}(\gamma, \tau^2)$ be independent random variables. Then the random variable $Z=X+Y$ has $\mathcal{N}(\mu+\gamma,\sigma^2+\tau^2)$ distribution. This idea is formalized using [[Convolution|convolutions]]. 
 
**Theorem: (Statistical [[Convolution]])** If $X$ and $Y$ are independent continuous random variables with pdfs $f_X(x)$ and $f_Y(y)$, then the pdf of $Z=X+Y$ is $$f_Z(z) = \int_{-\infty}^\infty f_X(x)f_Y(z-x)\,dx.$$Similar equations can be derived for operations other than summation.  



