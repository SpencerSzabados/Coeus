---
title: A neural network classifier based on Dempster-Shafer theory
authors: T. Denoeux
year: 2000
---

# Overview 
The author proposes a method of classifying input vectors using [[Belief functions]] using either class prototypes or a given set of training data; moreover, this method can be implemented as a [[Artificial neural networks|neural network]] or a network of [[Radial basis function|radial basis functions]] (radial basis function network). 


# Primary results
To begin with the author considers a training data set $X=\{(x_1,y_1),(x_2,y_2),\dots,(x_N,y_N)\}$ of vector label pairs with $y_i\in\{C_1,\dots,C_K\}$ is the set of potential classes which make up the frame of discernment $\Omega$, with basic belief assignments of the form $m:\mathcal{P}(\Omega)\to [0,1]$. The proposed method then attempts to classify a new input $x$ by combining the class belief assignment (evidence) provided by each training data point with respect to a monotonically decreasing function of the distance between $x$ and each training point (as done in [[@Mortier_2021]]). Specifically, the portion of belief that $x$ belongs to the same class as $x_i$, which we can assume to be $C_p$, with $x_1$ a distance $d_1=\|x_1-x\|$ from $x$, is $$\begin{align*}m_i(C_p) &= \alpha g_p(d_1)\\ m_i(\Omega) &= 1-\alpha g_p(d_1)\\ m_i(A) &= 0 \text{ for all }A\in\mathcal{P}(\Omega)\backslash \{\Omega,C_p\}\end{align*}$$where $0<\alpha<1$ and $g$ is a monotonically decreasing function that satisfies $g(0)=1$ and $\lim_{d\to \infty}g(d)=0$.

It is unlikely that every training data point will be sufficiently related (close) to $x$ to be worthwhile to process during prediction, hence the author limits the scope of computation by only exploring the $k$-[[Nearest-neighbour methods|nearset-neighbours]] of $x$, say $N_k(x)$.

The cumulative (total combined belief) provided by all elements of $N_k(x)$ for each individual class can be computed as the functional expression $$m=\oplus_{x_i\in N_k(x)} m_i.$$At each point in the feature space, the width of the interval $[bel(C_p),pl(C_p)]$ is equal to $m(\Omega)$, which expresses the amount of belief that could not be committed to any singular class due to a lack of available evidence; this interval is larger for points that are further away from known examples. This _ignorance_ value is later used in the papers discussion on sensor (classifier) fusion.

From this, to avoid Duch books, the [[Belief functions#Pignastic approach (Transferable belief model)|pignastic probably]] of $x$'s membership to any individual class, say $C_p$, is constructed by uniformly distributing any mass associated with $\Omega$ (ignorance); that is, $$BelP(C_p) = m(C_p)+\frac{m(\Omega)}{K}.$$
Then, under the assumption of binary $\{0,1\}$ losses, the prediction that minimizes risk corresponds to selecting the class with the largest pignastic probability.


## Prototype based utility optimization approach 
Moving on from this, the author outlines a procedure for utilizing a set of class prototypes $P_1,P_2,\dots,P_K$, which server as templates for class membership, opposed to a set of training values. Specifically, each prototype $P_i$ possess weighted membership (what is called _utility_ in other papers) $u_{i,p}$ to each class $C_p$ with the normalizing constraint $\sum_{p=1}^K u_{i,p}=1$. The basic belief assignment for $x$'s membership to a given class is then computed in a similar fashion as before, but with the addition of the new utility term; that is, $$\begin{align*}m_i(C_p) &= \alpha_iu_{i,p} g_p(d_1)\\ m_i(\Omega) &= 1-\alpha g_p(d_1)\end{align*}$$and $$\sum_{A\subseteq\Omega}m_i(A)=\sum_{p=1}^K m_i(C_p)+m_i(\Omega)=1.$$Note that, both the utility values and form of the prototypes (vectors of weights) are learned via backpropagation using a training data set as with the previous method or via a [[Classification and clustering#Clustering|clustering]] method; the exact calculations for this are provided in the papers appendix. Thus, the only difference between this method and the initial one is that after these values are learned we do not have to maintain the complete set of training values in order to perform inferences.

As before, the basic belief assignments are combined using either [[Belief functions#^58651b|Dempsters combination rule]] or [[Belief functions#^dc37a7|Conjunctive combination rule]]; for the first that is, $$m = \oplus_{i=1}^N m_i.$$
Then again, in the case of $\{0,1\}$ loss, the prediction that minimizes risk corresponds to selecting the class with the maximum mass; i.e., $$C = \arg\max_{C_p\in\Omega}m(C_p).$$

# Generalized decision criteria
For a loss function $L(C_P,C_i)$, which is taken to be a function with range $[0,1]$ that outputs a non-zero value for assigning $x$ the class of $C_p$ when its true class is $C_i$, the risk resulting from the selection of a class $C_p$ which has the pignastic probability $BetP(C_p)$ is given as $$R[C_p] = \sum_{C_i\in\Omega}L(C_p,C_i)BetP(C_i)=\sum_{A\subseteq \Omega}\frac{m(A)}{|A|}\sum_{C_i\in A}L(C_p,C_i).$$

The strategy of selecting the class that minimizes risk then brings about different decision rules. 

In particular, again for $\{0,1\}$ loss we get the risk values $$\begin{align*}R[C_p] = 1-BetP(C_p)=1-M(C_p)-\frac{m(\Omega)}{K}\end{align*}.$$And the choice of assigning $x$ to the class with largest pignastic probability can then be made based on  thresholding by a loss value, $L_0$, of choosing to reject the classification.


# Classifier (sensor) fusion
The authors of this paper also explore methods of fusing the output of classifiers that were separately trained in order to obtain a classifier that is more robust. This problem is explored first in the [[Bayesian probability theory|Bayesian sense]] then using Dempster-Shafer theory as seen in [[Evidence base classification#Classifier fusion methods|belif based classifier fusion]]. 

The evidential fusion method outperformed all other methods tested experimentally for test conducted using noisy input data.