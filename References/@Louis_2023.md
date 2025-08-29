---
doc type: Research paper summary
title: On sampling with approximate transport maps
authors: Louis Grenioux, Alain Oliviero Durmus, Eric Moulines, Marylou Gabrié
year: "2023"
last read: 2023-08-21 Mon
tags:
  - machine_learning
  - statistical_learning
  - random_sampling
  - flow
---
___

# Overview
This paper focuses on analysing the [[Monte Carlo simulation#^549186|mixing time]] of Important Sampling and [[Monte Carlo simulation#Markov chain Monte Carlo|Markov chain Monte Carlo]] methods when using [[Normalizing flows]], in particular triangular flows (autoregressive), to learn a proposal distribution, in terms of the push forwards measure, that is sufficiently close to the desired stationary distribution. Notably, the authors do not propose new methods for increasing the accuracy of estimates learned flows, but derive bounds on mixing time under very lose assumptions placed on (TODO).

TODO - are the authors assuming that we have a analytical formulation of the target distributions? This would be strange in most ML settings are we typically only have sample data to form empirical distributions estimates from etc.
    - The authors are interested in the situations where samples from the target distribution are not available beforehand when training flows for sampling. What do they mean, how do you fit the flow to the target when you only have iid samples from the sampling distributions that gets pushed to the target? They are using the reversed KL divergence to train the flow by pushing iid samples from $\rho$ trough the push-forwards (the flow) to the target distribution $\pi$, where $\pi$ is assumed to be given so that the aforementioned can be evaluated.
    - It is stated in the appendix they use various types of flow models, selected based on the problem being modeled, which where trained using the Adam optimizer. 

The paper concludes that multimodal target distributions can be effectively modeled using the proposed flow-based proposal acceleration method up to moderately high dimensions (TODO - what bound?).


# Primary results

## Sampling schemes considered 


## Bounds on the quality of flow
As previously known, see [[@Jaini_2020]] [[@Salmona_2022]], learning the exact flows from unimodal distributions to multimodal targets can be difficult or impossible. The difficulty of this task can be characterized, according to the authors, by the bi-Lipschitz constant required to construct the unique increasing flow (see TODO) between distributions. 

**Lemma:** Let the target distribution be Gaussian mixture of the form $d\pi=\frac{1}{2}\mathcal{N}(-\mu,\sigma^2)+\frac{1}{2}\mathcal{N}(\mu,\sigma^2)$ with $\mu>0$ and $\sigma>0$, and let the sampling distribution be $d\rho=\mathcal{N}(0,1)$. The unique increasing flow mapping $\pi$ to $\rho$, denoted $T$, has bi-Lipschitz constant $$\frac{dT^{-1}}{dz}(0)=\sigma \exp\left(\frac{\mu^2}{2\sigma^2}\right)\leq BiLip(T).$$
_Proof_: (This proof and lemma are limited to densities supported on $\mathbb{R}$. The authors let $T$ be the unique increasing flow (as given in [Bogacheve:2005]) from $\rho$ to $\pi$ (general distributions) and then compute the bi-Lipschitz constant by application of the chain rule.)

TODO - I think I've see a result exactly like this in another paper. [[@Salmona_2022]]?

Moreover, in [Cornish etal. 2020], it was shown that if the support of the sampled distribution $\rho$ and target distribution $\pi$ differ, then, in the limit, the homeomorphism $T_\sharp\mu$ which pushes $\rho$ to $\mu$ has a unbounded bi-Lipschitz constant.

Consequently, as neural network approximations (or exact implementations) of normalizing flows make use of [[Activation functions|activation functions]] that are contraction mappings (e.g., ReLu) the resulting flows necessarily have bounded bi-Lipschitz constants, and therefore cannot perfectly approximate any given target distribution.


## Mixing time analysis of Metropolis algorithm
To explore the impact of dimension on the quality of the learned flow and sampling the authors examine the mixing time for the (independent) [[Monte Carlo simulation#Metropolis algorithm|Metropolis algorithm]] under local approximation conditions.

**Problem statement:** Consider a [[s-Concave densities#^85184b|log-concave]] target distribution $\pi$ and a proposal distribution $\rho$ with density $d\rho$. What is the mixing time of the Metropolis algorithm with importance weighting function $$w(x)=d\pi(x)/d\rho(x)$$ under the following assumptions: (1) for any $R\geq 0$, there exists a $C\geq 0$ such that for any $x,y\in B_R(0)=\{z\mid \|z\|<R\}$ the inequality $|\log w(x)-\log w(y)|\leq C|x-y|$ holds; i.e., $w$ is locally log-concave and Lipchitz, with $C$ representing how closely $\rho$ approximate $\pi$. (2) $-\log d\pi(x)$ is [[Convex functions#^d1ebf5|m-strongly convex function]] on $\mathbb{R}^d$ and is minimized at $x=0$.

Under the above setup, the authors derive the following theorem:

**Theorem:** Let $0<\epsilon <1$ and $\mu$ a $\beta$-warm distribution with respect to $\pi$, and let $\rho$ be $\mathcal{N}(0,\sigma^2I)$ be the proposal distribution. Moreover, suppose we can bound the constant above as $C\leq \log(2\sqrt{m})/32$ when $$r\sqrt{d}\left(1+\frac{|\log^\alpha(\epsilon/\beta)|}{d^{\alpha/2}}\right)\max\left\{\sigma,\frac{1}{\sqrt{m}}\right\} \leq R$$for some chosen constant $r\geq 0$ and exponent $\alpha >0$. The mixing time for the Metropolis algorithm is important weighting (sampling) is bounded by $$\tau_{mix}(\mu,\epsilon)\leq 128\log(2\beta/\epsilon)\max\left\{1,\frac{(128C)^2}{m\log^2(2)}\right\}.$$
The above theorem, after substituting $\sigma=1+\gamma$, tells us that in order to achieve total variation distance less than $\epsilon$ after $N$ steps $\gamma$ must decrease at a rate of $O(1/d)$ per iteration.

More generally, the authors consider analysing the mixing time of the Metropolis algorithm with target distribution $\pi$ and proposal $\rho$ supported on $\mathbb{R}^d$  with respect to the Lebesgue measure.


# Experimental results
It is shown experimentally that Important sampling using a learned proposal distribution (Neural-IS) and using said learned proposal in MCMC sampling outperforms the so named neurtra-MCMC samplers, which make use of the push-backwards, considered for multimodal targets in high dimensions, with only the latter recovering the correct distribution (histograms) up to dimension 256.


## Training methodology 


# Connections