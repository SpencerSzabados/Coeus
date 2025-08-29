---
title: Efficient set-valued prediction in multi-class classification
authors: Thomas Mortier, Marek Wydmuch, Krzysztof Dembczyński, Eyke Hüllermeier, Willem Waegeman
year: 2021
---

Q: Can we genialize the class of functions that $g$ belongs to? For instance s-concave functions. Can you construct a counter example to show the given class of functions for $g$ is the best class you can use?
Q: Conformal predictions, predictions that are certain to contain the true value you are looking for.
Q: The authors assume perfect training data with single class membership, as was utilized in [[@Tong_2021]]. Could one come up with a method of using evidence (eg utility functions) to better train networks with noisy training data or imperfect training data. This related to what my supervisor said about the given algorithm; are they training the estimates for $p_1,p_2,\dots, p_k$ simultaneous with the values for their utility function using $g$ or are they doing it in two stages? If you could train in one stage they perhaps you could learn better estimates for these values.

---
# Overview
In the face of uncertainty multi-class [[Classifiers]] should return a set of candidate classes ([[Classification and clustering#Set-valued (multi-set) classification|set-valued classification]]) opposed to a single class label; provided the returned set is sufficiently small as to still be beneficial. The aim of the paper in question according to the authors, is to develop optimization algorithms for multi-class classification were the set of possible actions includes assignment to any possible subset of the available classes where the objective being optimized is a family of utility functions, which express the preserved utility of assigning one subset over another; where utility is based, at least partly, on the inclusion of the true class in the final prediction.  

The method of performing set-valued classification considered is based on ([[Bayesian probability theory]]) utility functions, where any prediction is weighed on its inclusion of the true underlying class and the size of the prediction (detrimental to be large). A different approach, which is not considered in this paper but is mentioned, related to [[Conformal prediction]] where a set of covers containing the true set with a desired degree of probability are constructed.

[[Classification and clustering#Set-valued (multi-set) classification|Set-valued classification]] is related to the problem of uncertainty modeling in multi-class classification. Under this comparison, the developed work can be seen as a method of making predictions in the face of aleatoric uncertainty (where there is noise in the sample data that we based predictions on). The authors approach does not analyze epistemic uncertainty (where the data being predicted might come from a different or shifted population compared to the training data) See [[@Hullermeier_2019]].


# Primary results
Suppose we are given training data of the from $\{(X_i,Y_i)\}_{i=1}^N$ from an underlying distribution $P(X,Y)$ defined on $\mathcal{X}\times \mathcal{Y}$ where $\mathcal{Y}=\{C_1,\dots,C_K\}$ is a set of classes. Then the set of possible outputs from the classifier is $\hat{Y}\in \mathcal{P}(\mathcal{Y})\backslash \{\emptyset\}$; the empty set is removed as outlier rejection is not considered.

Under the above utility framework, the quality of a prediction $\hat{Y}$ is based on a utility function, say $u(c,\hat{Y})$, where $c$ corresponds to the true classes of the input being considered. The goal is then to find the prediction that maximizes the expected utility over all possible conditional class estimates; that is, we seek $$\begin{align}\hat{Y}^* = \arg\max_{\hat{Y}\in \mathcal{P}(\mathcal{Y})}E_{P(C|x)}[u(C,\hat{Y})] &= \arg\max_{\hat{Y}\in \mathcal{P}(\mathcal{Y})}\sum_{C\in \mathcal{Y}}u(C,\hat{Y})P(C|x)\\ &= \arg\max_{\hat{Y}\in \mathcal{P}(\mathcal{Y})}U(\hat{Y},P,u).\end{align}$$

There are many different definitions possible for utility functions, here the authors focus on utility function of the form $$u(C,\hat{Y}) = \begin{cases}g(|\hat{Y}|) & \text{ if } C\in \hat{Y}\\ 0 & \text{ otherwise,} \end{cases}$$which are characterized by a decreasing sequence (of weights used to bias prediction towards larger or smaller sets) of the form $(g(1),g(2),\dots,g(K))\in [0,1]^K$. This kind of utility function was use in [[@Tong_2021]].

It is shown that for the purposes of optimization the function $g$ should satisfy the following properties. Additionally, it is noted that comparisons between $g$ and precision are arguably not useful, as precision is not risk averse to large classifications and would therefore prefer larger classes over singleton set predictions despite available evidence. 

**Definition: (1/x convexity)** A sequence $g(1),\dots, g(K)$ is $(1/x)$-convex if $$1/g(s+1)\leq \frac{1/g(s)+1/g(s+2)}{2}$$for all allowable values of $s$. Note, any concave sequence will automatically be $(1/x)$-convex.

**Requirement:** It is required that $g(s)\geq 1/s$ for all allowable $s$; otherwise, any utility function $u$, defined as above, will reduce through optimization to only providing singleton set solutions which obviously undermines the purpose of utilizing $u$ in the selection procedure.

In particular, if $g$ is a sequence such that $g(1)=1$, then for any distribution $P$ we have:
  1) If $g(s)> 1/s$ for some $s>1$, then $\hat{Y}^*$ is not a solution of the optimization procedure;
  2) If $g(s)<1$ for all $s>1$, then the solution $\hat{Y}^*$ to the above optimization procedure is a singleton set and this solution is unique;
  3) If $g(s)=1/s$ for all $s$, then the solution $\hat{Y}^*$ is a singleton set.


**Theorem:** The exact solution to $\hat{Y}^*$ can be found by analyzing $K$ subset of $\mathcal{Y}$ opposed to $2^{|\mathcal{Y}|}$.
_Proof:_ To begin we have $P(\hat{Y}|x)=\sum_{C\in \hat{Y}} P(C|x)$ and so the expected utility provided by $\hat{Y}$ can be written as $$\begin{align}\sum_{C\in\mathcal{Y}}u(X,\hat{Y})P(C|x ) &= \sum_{C\in\hat{Y}}u(X,\hat{Y})P(C|x) + \sum_{C\notin\hat{Y}}u(X,\hat{Y})P(C|x)\\ &= g(|\hat{Y}|)P(\hat{Y}|x).\end{align}$$Consequently we can write $$\hat{Y}^* = \arg\max_{\hat{Y}\in \{\hat{Y}^*_1,\hat{Y}^*_2,\dots,\hat{Y}^*_K\}}g(|\hat{Y}|)P(\hat{Y}|x),$$where $\hat{Y}^*_i = \arg\max_{|\hat{Y}|=i}g(i)P(\hat{Y}|x)$. $\square$

This procedure can performed efficiently by sorting the conditional class probabilities in decreasing order and only considering the most probable prediction for a particular cardinality. From this theorem, provided we can compute the requisite probabilities efficiently, we only need to examine $K$ total subsets during the optimization of $\hat{Y}^*$. This can be further improved if we adhere to the convexity requirement.

**Theorem:** If $g$ is a decreasing $(1/x)$-convex sequence, then for any $s\in\{1,\dots,K\}$ we have $$U(\hat{Y}^*_s,P,u)>U(\hat{Y}^*_{s+1},P,u)\Rightarrow U(\hat{Y}^*_{s+1},P,u)>U(\hat{Y}^*_{s+2},P,u).$$
Consequently, once the calculated optimal utility for a prediction decreases after an increment of prediction size we do not need to consider any larger predictions, as we have found the final prediction cardinality that needs to be considered.


## Algorithmic solutions
The first algorithm proposed is exact and returns the Bayes-optimal solution in $O(K\log K)$ time. A later algorithm is approximate and works based of off truncating the exploration of prediction size (among other things).


# Empirical results
Comparisons between different set-valued text classification data sets and image methods are presented. The proposed method of utility maximization proves to be competitive and superior in many instances to other existing methods or modification therein, such as outputting a fixed number of classes from a classifier that typically only outputs the maximal class.

