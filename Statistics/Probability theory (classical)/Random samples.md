---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - random_sampling
  - statistics
references:
  - "[[@Casella_2001]]"
---
---
# Overview
Random samples are a fundamental idea in statistics and estimation.

**Definition: (Random sample)** The random variables $X_1,X_2,\dots,X_N$ are called a _random sample of size $N$ from the population_ $f(x)$ if $X_1,X_2,\dots,X_N$ are mutually independent [[Random variables#^5ceb15|random variables]] and the marginal pdf (or pmf) of each $X_i$ is the same function $f(x)$; $X_1,\dots,X_N$ are also called _independent and identically distributed random variables_ (i.i.d) with pdf (or pmf) $f(x)$. ^fa048e

Under the random sampling model of a random variable, $X$, with distribution $f(x)$ each $X_i$ is an observation on the same variable; meaning each is an observation of the form $X_i=x$ with the same marginal distribution. Thus, another way of thinking about a random sample is to consider a sample set $x_1,x_2,\dots, x_N$ of realized values of $X$ resulting from repeat sampling, assuming $f(x)$ to be fixed between samples. It follows that, the joint pdf (or pmf) of $X_1,\dots,X_N$ is given by $$f(x_1,\dots x_N) = f(x_1)f(x_2)\dots f(x_N) = \prod_{i=1}^N f(x_i).$$ 
Note, a sample drawn from a finite population without replacement, see [[Basic counting]], does not satisfy all the conditions for a random sample. As draws are no longer mutually independent, as the marginal distribution of each sample depends on the results of those before it; e.g., for a second draw, $X_2$, we must calculate the marginal distribution as $$P(X_2=x) = \sum_{i=1}^S P(X_2=x|X_1=x_i)P(X_1=x_i),$$for a population of size $S$.

With that said, if the finite population size is large compared to the sample size, $X_1,\dots,X_N$ then it can be said to be _nearly independent_, provided the marginal distribution of $X_i$ given $X_1,\dots,X_{i-1}$ is not too different from that of $X_i$. In such a case, probability calculations can often be approximated by not accounting for conditionalities; see [[Random samples#Sampling convergence|sampling convergence]].

# Sums of random variables from random samples
Often you need to know the distribution of a sum or product of random samples. This is related to [[Statistical transformations]], but in this setting we are dealing iwth 

**Definition: (Sample statistic)** Let $X_1,\dots,X_N$ be a random sample of size $N$ from a population and let $T(x_1,\dots,x_N)$ be a real-valued (or vector-valued) function whose domain includes the sample space of $X_1,\dots,X_N$. Then the random variable or (random vector) $Y=T(X_1,\dots,X_N)$ is called a _statistic_. The probability distribution of a statistic $Y$ is called the _sampling distribution of_ $Y$. ^1176b9

This definition is really quite general with the only restriction being that a test statistic cannot depend directly on a parameter being estimated from the underlying population that the sample is drawn from. It is important to note the probability distribution of $Y$ is not, except for the trivial identity distribution, the same as that of $X$; e.g., $Y$ may range over a different set of values than $X$ with the frequency of these values depending on the size of $N$ and the sampling procedure used - with or without replacement etc.

A important aspect of sample statics (estimators) is its long run behaviour, which is referred to as the consistency of the estimator. 

**Definition: (Consistency of estimator)** An estimator $T$ of a parameter $\theta$ is said to be _consistent_, if it [[Random samples#Convergence in probability|converges in probability]] to the true value of the parameter; that is, the  $T(x_1,\dots,x_N)$ is consistent, if for a sequence of random samples $\{X_1,\dots,X_N\}$ the associated sequence of statistics $\{T_N\}$, in which each is based on the first $N$ sample values, converges to the true value of $\theta$, i.e.,  $$\lim_{N\to \infty}T_N = \theta,$$or equivalently, for any $\epsilon>0$ we have $$\lim_{N\to\infty}P(|T_N-\theta|>\epsilon)=0.$$

Two common statistics for summarizing a statistic, and for estimating parameters of the underlying population of $Y$, are the sample mean and variance: 

**Definition: (Sample mean)** Let $X_1,\dots,X_N$ be a random sample, the sample mean (average) is given by $$\overline{X} = \frac{1}{N}\sum_{i=1}^N X_i.$$
**Definition: (sample variance)** Let $X_1,\dots,X_N$ be the realized values of a random sample. The sample variance (or standard deviation) is $$s^2 = \frac{1}{N-1}\sum_{i=1}^N (X_i-\overline{X})^2.$$
The sample mean and variance share similar properties to their population counterparts. ^52b789

Note, the sample variance is divided by $N-1$ rather than $N$. This is done to derive an unbiased estimator of the variance, the derivation of which can be seen by following the calculation of the sample expectation $$\begin{align}E[s] &=E\left[\frac{1}{N}\sum_{i=1}^N(x_i-\bar{x})^2\right]\\
&=E\left[\frac{1}{N}\sum_{i=1}^N (x_i^2-2x_i\bar{x}+\bar{x}^2)\right]\\ &=E\left[\frac{1}{N}\sum_{i=1}^Nx_i^2 - \frac{2\bar{x}}{N}\sum_{i=1}^N x_i + \frac{\bar{x}^2}{N}\sum_{i=1}^N1\right]\\ &=E\left[\frac{1}{N}\sum_{i=1}^Nx_i^2 - \bar{x}^2\right]\\ &=E\left[\frac{1}{N}\sum_{i=1}^Nx_i^2 - \left(\frac{1}{N}\sum_{i=1}^Nx_i\right)^2\right]\\ &=E\left[\frac{1}{N}\sum_{i=1}^Nx_i^2 - \frac{1}{N^2}\left(\sum_{i=1}^Nx_i^2 - \sum_{\substack{i=1\\ i\neq j}}^N\sum_{j=1}^N x_ix_j\right)\right]\\ &=\frac{1}{N}\sum_{i=1}^N E[x_i^2] - \frac{1}{N^2}\left(\sum_{i=1}^N E[x_i^2] - \sum_{\substack{i=1\\ i\neq j}}^N\sum_{j=1}^N E[x_ix_j]\right)\\ &=\frac{1}{N}\sum_{i=1}^N E[x_i^2] - \frac{1}{N^2}\left(\sum_{i=1}^N E[x_i^2] - \sum_{\substack{i=1\\ i\neq j}}^N\sum_{j=1}^N \mu^2\right)\quad \text{($E[x_ix_j] = \mu^2$ by i.i.d)}\\ &=\frac{1}{N}\sum_{i=1}^N E[x_i^2] - \frac{1}{N^2}\left(\sum_{i=1}^N E[x_i^2] - (N^2-N) \mu^2\right)\\ &=\frac{N-1}{N^2}\sum_{i=1}^N E[x_i^2] - \frac{N-1}{N}\mu^2\\ &=\frac{N-1}{N}E[x_i^2] - \frac{N-1}{N}\mu^2\\ &=\frac{N-1}{N}(\sigma^2+\mu^2)-\frac{N-1}{N}\mu^2\\ &=\left(\frac{N-1}{N}\right)\sigma^2.\end{align}$$Thus, in order to correct the present bias the denominator in the calculation of sample variance should be replaced by $N-1$, this is called _Besse's correction_. ^88238b

For absolute clarity, it is worth pointing out the _subtle_ difference between the sample mean $\overline{X}$ which is a random estimates the mean of sample distribution of $Y$ and the sample mean $\overline{x}$ of a particular sample. If $X_1,\dots,X_N$ is a random sample, then $\overline{X}$ is an estimator of the mean of the sample distribution of $Y$. Whereas, if we have a particular realization of values $x_1,\dots,x_N$, then $\overline{x}$ is simply the mean of these values, which for a sufficiently large $N$ will be a good estimator of $Y$'s mean just as with $\overline{X}$ but the later is not a random variable unlike the first. 

Continuing, if $X_1,\dots,X_N$ are random variables (not necessarily independent) with mean $\mu$ and variance $\sigma^2$, then $$0\leq E[s^2]\leq \frac{N}{N-1}\sigma^2$$is the expected range of values the sample variance can take on, which varies as a result of any dependence between the random variables.  


**Theorem:** Let $x_1,x_2,\dots,x_N$ be any numbers (observations) and $\overline{x}$, the sample mean, be given. Then 
   1) $\min_a \sum_{i=1}^N(x_i-a)^2 = \sum_{i=1}^N (x_i-\overline{x})^2$ or equivalently for any $a$ we have $\sum_{i=1}^N(x_i-a)^2 \geq \sum_{i=1}^N (x_i-\overline{x})^2$;
   2) $(n-1)s^2 = \sum_{i=1}^N x_i^2 - n\overline{x}^2$.

**Lemma:** Let $X_1,X_2,\dots,X_N$ be a random sample (i.i.d) from a population and let $g(x)$ be a function such that $E[g(X_1)]$ and $Var[g(X_1)]$ both exists. Then $$E\left[\sum_{i=1}^N g(X_i)\right] = n(E[g(X_1)]),$$ and $$Var\left[\sum_{i=1}^Ng(X_i)\right] = n(Var[g(X_1)]),$$as each $X_i$ is identically distributed and by application of linearity of expectation.

Consider repeatedly drawing random samples of size $N$ from a population with mean $\mu$ and computing the sample mean for each random sample; that is, consider a random sample of the from $\overline{X}_1,\dots,\overline{X}_m$. These values follow a distribution with mean and variance that depend on that of the underlying population, as shown in the following theorem.

**Theorem:** Let $X_1,\dots, X_N$ be a random sample from a population with mean $\mu$ and variance $\sigma^2$. Then the random variable $\overline{X}$ is distributed according to:
   1) $E[\overline{X}] = \mu$;
   2) $Var[\overline{X}] = \sigma^2/N$;
   3) $E[s^2] = \sigma^2$.
_Proof:_ See [StackExchange-BruceET](https://math.stackexchange.com/a/1898502).

**Corollary:** Let $X_1,\dots, X_N$ be a random sample from a population with mean $\mu$ and variance $\sigma^2$. Then $E[X_i\overline{X}] = \sigma^2/N + \mu$ for any $i=1,\dots,N$.
_Proof:_ See [StackExchange](https://math.stackexchange.com/questions/1137479/can-anyone-solve-this-exi-x-bar).


# Order statistics 
**Definition: (Order statistics)** The _order statistics_ of a random sample $X_1,\dots,X_N$ are the sample values placed in ascending order, denoted $X_{(1)},\dots,X_{(N)}$. In particular, $$\begin{align}X_{(1)} &= \min_{1\leq i\leq N} X_i,\\ X_{(2)} &= \text{second smallest $X_i$},\\ &\vdots\\ X_{(N)} &= \max_{1\leq i\leq N}X_i\end{align}$$
**Definition: (Sample median)** The sample median (or simply median), $Med$, is the number such that approximately one-half the observations fall on either side of it; that is, $$Med = \begin{cases}X_{((N+1)/2)} & \text{if $N$ is odd}\\ (X_{(N/2)}+X_{((N+1)/2)})/2 & \text{if $N$ is even.}\end{cases}$$
The sample median is less susceptible to the presence of outliers in a sample than the sample mean. In addition, unlike the sample mean, the sample median is chosen as an element in the set of observations (provided you decide not to average in the case where $N$ is even as is sometimes done). It is also worth recalling that a sample can have multiple median elements, i.e., the median element need not be unique. 

Intuitively, for sufficiently nice distributions (single model and symmetric), the median should be very close to the expected value of the distribution; that is, for utmost clarity, medians and expected values can by identified with one another for select distributions but are not equivalent quantities in general.

**Definition: (Quantiles)** Let $F$ be a cdf of the random variable $X$. By construction (or wlg) $F$ is monotonically increasing, so possesses an (generalized) inverse $F^{-1}$. Then $F^{-1}(\alpha)$, with $0\leq \alpha\leq 1$, is the value $X=x$ such that $P(X\leq F^{-1}(\alpha))=\alpha$; this is called the $\alpha$-quantile of $F$; Note, there are several different definitions of quantiles that are used in literature but this is one of the most standard. ^52c883

e.g.,) The median, in the case of a continuous random variable, is the $\alpha = 0.5$ quantile. 

**Theorem: (Discrete order statistic probabilities)** Let $X_1,\dots,X_N$ be a random sample from a discrete distribution with pmf $f_X(x_i)=p_i$, where $x_1<x_2<\cdots$ are the possible values of $X$ in ascending order. Define the cumulative probabilities $$P_0=0,\, P_1=p_1,\, P_2=p_1+p_2, \dots,\, P_i = p_1+\cdots p_i,\dots$$ and let $X_{(1)},\dots,X_{(N)}$ denote the order statistics from the sample. Then $$P(X_{(j)}\leq x_i) = \sum_{k=j}^N\binom{N}{k}P^k_i(1-P_i)^{N-k},$$and $$P(X_{(j)} = x_i) = \sum_{k=j}^N \binom{N}{k}(P^k_i(1-P_i)^{N-k} - P^k_{i-1}(1-P_{i-1})^{N-k}).$$

**Theorem:** Let $X_{(1)},\dots,X_{(N)}$ denote the order statistics of a random sample, $X_1,\dots,X_N$, from a continuous population with cdf $F_X(x)$ and pdf $f_X(x)$. Then the pdf of $X_{(j)}$ is $$f_{X_{(j)}}(x) = \frac{N!}{(j-1)!(N-j)!}f_X(x)F_X(x)^{j-1}(1-F_X(x))^{N-j}.$$


# Sampling convergence 


## Convergence in probability 
**Definition: (Probability convergence)** A sequence of random variables, $X_1,X_2,\dots$, _converges in probability_ to a random variable $X$ if, for every $\epsilon >0$, $$\lim_{N\to \infty}P(|X_N-X|\geq \epsilon) = 0\quad\text{or}\quad \lim_{N\to \infty}P(|X_N-X|<\epsilon)=1.$$ ^9a4542

Frequently, statisticians are concerned with finding constant limits for random variables, such as sample means. The most famous result being the following:

**Theorem: (Weak law of large numbers)** Let $X_1,X_2,\dots$ be a iid random variables (random sample of unspecified length) with $E[X_i]=\mu$ and $Var[X_i]=\sigma^2$ finite. Then, for every $\epsilon >0$, $$\lim_{N\to \infty}P(|\overline{X}_N-\mu|<\epsilon)=1;$$that is, $\overline{X}$ converges in probability to $\mu$ as the random sample size increases to infinity.

The property expressed by WLLN, that a sequence sampling the same quantity approaches a constant as the sample size grows to infinity, is called _consistency_.

The following theorem relates functions of random variables to sequences of convergent random variables.

**Theorem:** Suppose that $X_1,X_2,\dots$ converges in probability to a random variable $X$ and that $h$ is a continuous function. Then $h(X_1),h(X_2),\dots$ converges in probability to $h(X)$.


## Almost sure convergence
A type of convergence that is stronger than convergence in probability, is almost sure convergence (sometimes called _convergence with probability 1_).

**Definition: (Almost sure convergence)** A sequence of random variables ,$X_1,X_2,\dots$, _converges almost surely_ to a random variable $X$ if, for every $\epsilon >0$, $$P\left(\lim_{N\to \infty}|X_N-X|<\epsilon\right)=1.$$
This definition states, that $X_n$ converges to $X$ almost surely if the functions $X_N(s)$ converge to $X(s)$ for all $s$ in the sample space $S$ except perhaps for $s\in A$, where $A\subset S$ with $P(A)=0$.

**Theorem:** Almost sure convergence implies convergence in probability.

The converse of this theorem does not hold in general; however, if a sequence converges in probability, is is possible to find a subsequence that converges almost surely.

**Theorem: (Strong law of large numbers)** let $X_1,X_2,\dots$ be iid random variables with $E[X_i]=\mu$ and $Var[X_i]=\sigma^2$ finite. Then, for every $\epsilon >0$, $$P\left(\lim_{N\to \infty}|\overline{X}_N-\mu|<\epsilon\right)=1;$$that is, $\overline{X}_N$ converges almost surely to $\mu$.


## Convergence in distribution 
**Definition: (Converges in distribution)** A sequence of random variables $X_1,X_2,\dots$, with cdfs $F_{X_1},F_{X_2},\dots$ _converges in distribution_ (or is said to _weakly converge_) to a random variable $X$ with cdf $F_X$ if $$\lim_{N\to \infty}F_{X_N}(x) = F_X(x)$$for all points $x$ where $F_X(x)$ is continuous. ^f340e3

Note here it is not _really_ the random variables themselves that converge but their cdfs converging. As such, convergence in distribution is one of the weaker forms of statistical convergence as it is implied by convergence in probability. 

**Theorem:** If the sequence of random variables, $X_1,X_2,\dots$, converges in probability to a random variable $X$, the sequence also converges in distribution to $X$; that is, convergence in probability implies convergence in distribution. 

**Theorem:** The sequence of random variables, $X_1,X_2,\dots,$ converges in probability to a constant $\mu$ if and only if the sequence also converges in distribution to $\mu$.

The sample mean is one statistic whose sampling behaviour we wish to study in more detail in light of the above theorem, specifically 

**Theorem: (Weak central limit theorem)** Let $X_1,X_2,\dots$ be a sequence of iid random variables whose mgfs (moment generating functions) exist in a neighbourhood around zero (or characteristic functions). Let $E[X_i]=\mu$ and $Var[X_i]=\sigma^2>0$, both finite. Define $\overline{X}_N=(1/N)\sum_{i=1}^N X_i$. Let $G_N(x)$ denote the cdf of $\sqrt{N}(\overline{X}_N-\mu)/\sigma$. Then for any $-\infty<x<\infty$, $$\lim_{N\to \infty}G_n(x) = \int_{-\infty}^\infty \frac{1}{\sqrt{2\pi}}e^{-y^2/2}\, dy.$$That is, $\sqrt{N}(\overline{X}_N-\mu)/\sigma$ has a limiting standard normal distribution.

The core conclusion of this theorem is that under no assumptions other than independence and finite variances $\overline{X}_N$ converges to a normal distribution under sufficiently large number of samples. Normality comes about from sums of "small" finite variance independent disturbances. A unfortunate limitation of CLT is it does not give us any indication of how large a sample must be for a good approximation of a normal distribution (and vice versa).

**Theorem: (Slutsky's)** If $X_N$ converges to $X$ in distribution and $Y_N$ converges to $a$ in probability, for $a$ constant, then 
   1) $Y_NX_N\to aX$ in distribution;
   2) $X_N+Y_N\to X+a$ in distribution. 




