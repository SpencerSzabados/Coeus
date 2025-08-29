A random measure is a function that forms a valid [[Measure spaces|measure]] for random elements (e.g., [[Random variables]]), which generalized the notion of [[Random variables]].

# Empirical measure
One of the most common random measures, at least in the context of [[Nonparametric statistics]], is the empirical measure which arises from the realization of a set of [[Random samples|random sample (or sequence)]].

**Definition: (Empirical distribution)** Let $X_1,X_2,\dots,X_N$ be a iid random sample that have values in $\mathcal{X}$ and are distributed according to a unknown [[Distribution functions of random variables#^c46bbe|distribution]] $p$. The empirical measure $p_N$ is defined for measurable subsets $A$ of $\mathcal{X}$ given by $$p_N(A) = \frac{1}{N}\sum_{i=1}^N\mathbb{I}\{X_i\in A\}.$$ See, [Wiki](https://en.wikipedia.org/wiki/Empirical_measure).

That is, if $f$ is a [[Measure spaces#^f47214|measureable function]], with respect to $p_N$, then the empirical measure maps $f$ to its empirical mean $$p_nf = \int_\mathcal{X}f\, dp_N =\frac{1}{N}\sum_{i=1}^N\int_{\mathcal{X}}f\,d\mathbb{I}\{X\in\{X_1,X_2,\dots,X_N\}\} =\frac{1}{N}\sum_{i=1}^N f(X_i).$$


