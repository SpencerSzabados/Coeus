Here we discuss techniques for constructing families of [[Fundamentals of probability theory#Distribution functions|distributions]] from known pdfs, via location shifting and scaling transforms (see more generally [[statistical transformations]])).


# Overview
The central theorem permitting these changes is the following:

**Theorem:** Let $f$ be any pdf and let $\mu$ and $\sigma>0$ be any given constants. Then the function $$g(x|\mu,\sigma) = \frac{1}{\sigma}f\left(\frac{x-\mu}{\sigma}\right)$$is a pdf.

**Definition: (Location family)** Let $f$ be any pdf. Then the family of pdfs $f(x-\mu)$, index by the parameter $\mu$, $-\infty < \mu < \infty$, is called the _location family_ with standard pdf $f$ and $\mu$ is called the _location parameter (or threshold parameter)_ of the family.

The name coming from the fact that $\mu$ shifts the mean of the distribution to the left or right of its original location. Hence, if $X$ is a random variable we have that $$P(a\leq X\leq B|0) = P(\mu-a\leq X\leq \mu+b|\mu),$$where the random variable $X$ has pdf $f(x)$ on the left of the equality and $f(x-\mu)$ on the right. Moreover, if $X$ is a random variable with pdf $f(x-\mu)$, then $X$ may be decomposed and written as $X=Z+\mu$, where $Z$ is a random variable with pdf $f(z)$; e.g., consider $X$ as some measured quantity, with $\mu$  representing the exact value of the quantity, and $Z$ the error in any measurement. This form of decompositions and error representation is frequently used in [[Overview of machine learning]] and [[Curve fitting]] methods for prediction accuracy assessment.

**Definition: (Scale family)** Let $f$ be any pdf. Then for any $\sigma>0$, the family of pdfs $(1/\sigma)f(x/\sigma)$, indexed by the parameter $\sigma$, is called the _scale family_ with standard pdf $f$, and $\sigma$ is called the _scale parameter_ of the family. 

In effect the parameter $\sigma$ either stretches the graph of $f$ (for values of $\sigma>1$) or compresses, spreads out the area of, the graph of $f$  (for values $\sigma<1$).

**Definition: (Location-scale family)** Let $f$ be any pdf. Then for any $\mu$, $-\infty<\mu<\infty$, and any $\sigma>0$, the family of pdfs $(1/\sigma)f((x-\mu)/\sigma)$ is called the _location-scale family_.

The following theorem relates the above transformations of a pdf to those [[Statistical transformations|transformations of random variables]] (e.g., functions of random variables). 

**Theorem:** Let $f$ be any pdf. Let $\mu$ be $-\infty<\mu<\infty$, and let $\sigma>0$. Then $X$ is a random variable with pdf $(1/\sigma)f((x-\mu)/\sigma)$ if and only if there exists a random variable $Z$ with pdf $f(z)$ and $X=\sigma Z+\mu$. 

**Corollary:** Let $Z$ be a random variable with pdf $f(z)$, and suppose $E[Z]$ and $Var[Z]$ exist. If $X$ is a random variable with pdf $(1/\sigma)f((x-\mu)/\sigma)$, then $$E[X] = \sigma E[Z]+\mu \quad\text{ and }\quad Var[X] = \sigma^2 Var[Z].$$Moreover, $P(X\leq x)=P\left(\frac{x-\mu}{\sigma}\leq \frac{x-\mu}{\sigma}\right) = P\left(Z\leq \frac{x-\mu}{\sigma}\right)$. Hence, if $P(Z\leq z)$ is easily calculable, then probabilities of $X$ may be easily obtained. 