In many experiments, and in analytical situations, it is easier to deal with a summary variable in place of original named observation data or structures specific to the particular experiment. Thus we often define a mapping from experimental results to a set of real numbers that summarize the collected data. An old-fashioned definition describes a random variable as a real variable that takes on its values by chance [[@Taylor_1998]].


**Definition: (Random variable)** A _random variable_ is a function, $X:S\to \mathbb{R}$, from a sample space $S$ into the real numbers; more specifically, given a probability space $(\Omega, \mathcal{B}, \mu)$, a random variable $X$ is a [[Measure spaces#^f47214|measureable function]] w.r.t. $\mu$, $X:\Omega\to\mathbb{R}$.   ^5ceb15

A _realization_ of a random variable is the result given by applying the random variable to an observed outcome (a [[Fundamentals of probability theory#^7d2bad|realized]] [[Fundamentals of probability theory#^4b13e7|event]]); the realization of a random variable is typically denoted using the lowercase letter assigned to the random variable itself.

In defining a random variable a new sample space is created (the range of the random variable). Thus, it must be shown there exists equivalence between the probability function defined on the original sample space and that defined in terms of the sample space associated with the random variable. Suppose $S = \{s_1,\dots,s_N\}$ is a sample space with probability function $P$. Define a random variable $X$ from $S$ with range $\mathcal{X} = \{x_1,x_2\dots,x_M\}$. The probability function $P_X$ on $\mathcal{X}$ is defined based on the desired condition that $X=x_i$ if and only if the random experiment results in an $s_i\in S$ such that $X(s_i)=x_i$. Hence, we define the _induced probably function_ of $X$ on $\mathcal{X}$ to be $$P_X(X=x_i) = P(\{s_j\in S\mid X(s_j)=x_i\}).$$
If $\mathcal{X}$ is uncountable, the induced probability function, $P_X$, is defined in terms of a range of values rather than a singleton; namely, for any set $A\subset \mathcal{X}$, $P_X(X\subset A) = P(\{x\in S\mid X(s)\in A\}).$

The induced probability function of a random variable $X$ is often abbreviated down to $P_X(x_i)$ or simpler still, in an abuse of notation, to $P(X=x_i)$  or $P(x_i)$ depending on the context.  

If a variable cannot be directly observed but only inferred about indirectly through other observable variables it is called a _latent variable_, with the later is called an _observable variable. ^b42b34

There are two main classes of random variables, those that take on discrete values and those that take on a continuum of values.

**Definition: (Discrete random variable)** A random variable $X$ is discrete if its [[Distribution functions of random variables#^1a548c|cumulative distribution function]] $F_x(x)$ is a step function in $x$; that is, a random variable $X$ is discrete if its image is countable. ^cc6415

**Definition: (Continuous random variable)** A random variable $X$ is _continuous_ if its [[Distribution functions of random variables|cumulative distribution function]] $F_X(x)$ is continuous in $x$ and differentiable everywhere except at possibly countably many points. (This last requirement that the the cdf is differentiable everywhere except possibly a countably many points can be somewhat ignored as it is a consequence of the definition of a continuous cdf through integration of a pdf.) ^1f3d1f


# Multiple random variables 
We need to know how to describe and use probability models that deal with more than one random variable at a time, as most experiments measure more than one characteristic per sampling; e.g., measuring the weight of a group of people would be represented as a set of realized values for each separate random variables, one per person. 

**Definition: (higher order random variable)** An $n$-_dimensional random vector_ is a function from a sample space $S$ into $\mathbb{R}^n$ (n-dimensional Euclidean space); that is, an $n$-dimensional random variable can be expressed as a multivariant function, $f:S\to \mathbb{R}^n$, with $f(\vec{s}) = (x_1,x_2,\dots,x_n)$.

**Definition: ([[Distribution functions of random variables#^0257fe|Random variable independence]])** Let $(X,Y)$ be a random vector with joint pdf (or pmf) $f(x,y)$ and marginal pdfs (or pmfs) $f_X$ and $F_Y$. Then $X$ and $Y$ are called _independent random variables_ if, for every $x$ and $y$, $$f(x,y) = f_X(x)f_Y(y).$$