---
title: Consistent multilabel classification
authors: Oluwasanmi O Koyejo, Nagarajan Natarajan, Pradeep K Ravikumar, Inderjit S Dhillon
year: 2015
---
---
# Overview
This paper discusses methods of evaluating the consistency (accuracy) of multi-label classification methods and proposes an efficient "drop in" framework.

A _classification metric_ is used to measure the utility, in the Bayes sense, of a classifier based on some desired behaviour; such metrics can be sampled using a simple dataset and then generalized to the population metric version when given the data distributions. 

There are two emerging ways to study classifier performance (population performance) based on utility: Decision Theoretic Analysis (DTA), in which utilities measure the expected performance of a classifier on a fixed-size test dataset, and Empirical Utility Maximization (EUM), where utilities are directly defined as functions of the population confusion matrix (matrix of true positives, false positives, etc). This paper proposes a combined generalized approach of these two methods, and shows that a Bayes optimal multilabel classifier for the studies metric can be expressed as a simple decision rule.


# Primary results
Consider a multilabel classification problem with $\{C_1,\dots,C_K\}$ possible labels and data inputs (instances) denoted $(x^{(i)},y^{(i)})\in\mathcal{X}\times\mathcal{Y}$. Encode the labels into a binary (dictionary) vector $y^{(i)}\in\mathcal{Y}=\{0,1\}^K$ with $y_j^{(i)}=1$ if and only if $x$ is associated with the $i$ label, and $y_j^{(i)}=0$ otherwise. 

Define the confusion values for the multilabel classifier $f$ (true positive etc) as $$\begin{align}TP(f_jx^{(i)})) = \mathbb{1}\{f_j(x^{(i)})=1,y^{(i)}_j=1\}, &\quad TN(f_jx^{(i)})) = \mathbb{1}\{f_j(x^{(i)})=0,y^{(i)}_j=0\}\\
FP(f_jx^{(i)})) = \mathbb{1}\{f_j(x^{(i)})=1,y^{(i)}_j=0\}, &\quad FN(f_jx^{(i)})) = \mathbb{1}\{f_j(x^{(i)})=0,y^{(i)}_j=1\}.\end{align}$$To generalize the statement of the given result, the authors consider a set of possible actions defined over all data points and all possible assignments by $f$, $$A_M(f) = \{TP(f_j(x^{i})), TN(f_j(x^{i})), FP(f_j(x^{i})), FN(f_j(x^{i}))\}^{K,N}_{j=1,i=1}.$$Then simple multilabel metric can be constructed as functions of the form $\phi:A_M(f)\to [0,\infty)$.

The population utility of a multilabel classifier $f$ is then defined as $$U(f,\phi,P) = \phi(\{E[A_n(f)]\}_{n=1}^M)$$with the expectation taken over iid draws from the joint distribution $P$; this generalizes EUM style classifiers for binary data. This differs from DTA which defines utility as $U(f,\phi,P)=E[\phi(\{A_n(f)\}_{n=1}^M)]$.

Thus the goal of a multilabel classifier that is attempting to maximize utilities of this nature is to find parameters such that $$f^* = \arg\max_{f:\mathcal{X}\to\{0,1\}^K}\{U(f,\phi,P)\};$$an estimator, $\hat{f}$, of this ideal classifier is consistent if $U(\hat{f},\phi,P)\to U(f^*,\phi,P)$ in probability ([[Random samples#^9a4542|converges in probability]]).


## Micro-averaging optimal classifier
The authors restrict their attention to metrics of the form (linear-fractional) $$\phi(TP,FP,FN,TN) = \frac{a_0+a_{11}TP+a_{10}FP+a_{01}FN+a_{00}TN}{b_0+b_{11}TP+b_{10}FP+b_{01}FN+b_{00}TN}$$with fixed parameter values.

The authors further resect their focus to micro-averaged utilities metrics of the from $$\phi_{micro}(\{A_n(f)\}_{n=1}^M) = \frac{1}{M}\sum_{i=1}^K\phi(TP_i,FP_i,TN_i,FN_i)$$
which can be reduced to the form above as $$\phi_{micro}(\{A_n(f)\}_{n=1}^M) = \frac{c_0+c_1TP(f)+c_2\gamma(f)}{d_0+d_1TP(f)+d_2\gamma(f)}$$where $\gamma(f)=\sum_{i=1}^K P(f_i(x^{(j)})=1)$ is the population probability that any input is correctly labeled by the classifier, see paper for constants.

**Theorem: (Bayes optimality rule)** Assuming the joint probability $P$ has density such that $dP=\mu dx$. Given constant values $c_0,c_1,c_2$ and $d_0,d_1,d_2$, define $$\delta^* = \frac{d_2U(f^*,\phi_{micro},P)-c_2}{c_1-d_1U(f^*,\phi_{micro},P)}.$$Then, the optimal Bayes classifier $f^*$ is given by the decision rules: 
  1) When $c_1>d_1U(f^*,\phi_{micro},P)$, $f_j^* = \mathbb{1}\{P(Y_j=1|X=x)>\delta^*\}$ for $j=1,\dots,K$; and 
  2) When $c_1<d_1U(f^*,\phi_{micro},P)$, $f_j^* = \mathbb{1}\{P(Y_j=1|X=x)<\delta^*\}$ for $j=1,\dots,K$.

That is, the optimal multilabel classifier can be obtained by thresholding the marginal instance-conditional class probability for each label with respect to the input, using the same threshold value for each. Thus, it suffices, in this situation, to learn the optimal value for $\delta^*$, which is a value within $[0,1]$ that depends on the metric and the label-wise instance-conditional marginal of $P$; in particular $$\delta^* = \arg\max_{\delta\in [0,1]}\{\phi_{mirco}(\hat{f}(x))\}$$with $\hat{f}=\{f_j(x^{(i)})=\mathbb{1}\{P(Y_j=1|X=x)>\delta\}\}$; a set of thresholding classifiers. 

The authors give a short algorithm for how to construct the optimal classifier for $\phi_{micro}$ in this setting. The authors refer the reader to [Reid - Composite binary losses (2010)] for how best to estimate $P(Y_j=1|X=x)$.

```pseudocode
Let S={(x,y)} be the train set
Let micro() be the metric function
_______________________________________________
Optimize_delta(S, micro())
    For i=1,...,k do
        Select training data matching label i, say S_i
        Split S_i into two sets E and D
        Estimate P(Y_i=1|X=x) using E
        Define f_i(x) = 1{P(Y_i=1|X=x) > delta}
    End
    Obtain delta* by solving argmax{micro(f_i(x))} over D
    Return the new function f_i(x)* = 1{P(Y_i=1|X=x) > delta*}
```