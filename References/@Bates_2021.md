---
title: Distribution-free, risk-controlling prediction sets
authors: Stephen Bates, Anastasios Angelopoulos, Lihua Lei, Jitendra Malik, Michael Jordan
year: 2021
---

# Overview
This paper looks at the problem of performing [[Classification and clustering#Set-valued (multi-set) classification|set-valued prediction]] where set predictions are made based on the sets computed risk compared against a user defined threshold. The risk associate with any given set is calibrated using a holdout set from the training data (or a separate set from the same distributions as the distribution which we are performing inferences on). More specifically, the returned sets are designed to have a distribution-free limit on their expected loss, with sets that exceed a user defined risk value not being output or the predictor rejects to output a prediction. The size of the predicted sets then depend on the accuracy of the classifier in question at a desired risk level; where a low accuracy classifier or high risk level necessitates the use of a larger holdout calibration set. 

The authors of this paper apply their derived method to [[Multi-label classification]] problems, and [[Hierarchical classification]] problems that were the focus of [[@Mortier_2022]]. The method developed is intended as a way of modifying existing black-box predictors, and as such is a very pragmatic approach. This is feasible due to the model only requiring the data used for calibration and testing (validation) to come from the same distribution, with no requirements placed on the data initially used to train the initial predictor $\hat{f}$ from which the set-valued predictor is developed form. 

The work in this paper is closely related to [[Conformal prediction]] (and tolerance regions) as the method seeks to provide finite-sample guarantees. However, there the authors makes use of prediction probability tolerances, rather than conformal guarantees.


# Primary results
Suppose we are given training data of the from $\{(X_i,Y_i)\}_{i=1}^N$ iid from an underlying distribution $P(X,Y)$ defined on $\mathcal{X}\times \mathcal{Y}$ where $\mathcal{Y}=\{C_1,\dots,C_K\}$ is a set of classes. Then for a input $x\in\mathcal{X}$ the authors consider a set-valued predictors $f:\mathcal{x}\to\Omega$ with $\Omega=\mathcal{P}(\mathcal{Y})$.

The authors assume a precise classification predictor $\hat{f}$ has been fitted on the training data using an established procedure, moreover, it is assumed that a index collection of set-valued predictors $\{f_\lambda\}_{\lambda\in \Lambda}$ is constructed based on $\hat{f}$ and obey the nesting constraint $\lambda_1<\lambda_2$ implies $f_{\lambda_1}(x)\subset f_{\lambda_2}(x)$. Given this, the authors focus on developing a predictive criteria based on risk for a set valued predictor $f$ that is constructed from $\hat{f}$. 

The construction of $\{f_\lambda\}_{\lambda\in\Lambda}$ used as an example in the paper, which is approximately optimal for loss values incurred by not including a specific class in the predictive set, follows a greedy procedure of building predictive sets out of discrete mappings. In particular, if $\hat{f}(y)$ is a given predictor, which is an estimate of $P(Y=y|X=x)$ the probability of $x$ belong to a specific class, then setting $\hat{\rho}(y,S)=L(y,S)\hat{f}(y)$ the set-valued predictors are constructed by thresholding against $\hat{\rho}(y,S)$.  

```pseudocode
Let lambda be the index of the desired set-valued predictor
Let rho be the conditional risk density defined above
let h be the step size for disretizing rho
___________________________
GreedySets(lambda, rho, h)
    F = emptyset
    T  = MAX //upper bound on loss (for bounded loss)
    While T > -lamda do
        T = T-Delta_lambda
        F = Union(F, {y not in F | rho(y,F)>T})
        
    return F   
```

Let $L:\mathcal{Y}\times\Omega\to\mathbb{R}_{\geq 0}$ be a monotonic [[Point estimation#^45314f|loss function]] based on a set-valued prediction and true underlying class. The losses considered must obey a nesting property akin to that of the set predictors, where set predictions $S_1\subset S_2$ imply $L(y,S_1)\geq L(y,S_2)$.

Then a classifier $f$ is called a $(\alpha, \delta)$-risk-controlling prediction set if, with probability at least $1-\delta$, $R[f(x)]\leq \alpha$ for all $x\in\mathcal{X}$. This error level $(\alpha, \delta)$ is specified by the user. 

Aside, this last requirement on the loss functions is somewhat unusual, as compared to other works related to set-valued prediction, as one typically tries to bias the predictor away from larger predictions [[@Mortier_2021]]. Moreover, how do the authors avoid this condition not reducing their method to being vacuous where a set-valued predictor $f$ that output $\mathcal{Y}$ would yeild the lowest risk? 

Lets assume we have access to a point-wise upper confidence bound for the risk function, that is, we know $$P(R[f_\lambda]\leq \hat{R}[f_\lambda])\geq 1-\delta$$where $\hat{R}[f_\lambda]$ is the upper confidence bound. Later in the paper the authors show methods of obtaining these bounds. From here, pick $$\hat{\lambda}=\inf\{\lambda\in\Lambda\mid \hat{R}[f_{\lambda'}]\leq \alpha \text{ for all }\lambda'\geq \lambda\}.$$This lambda corresponds to the selection of a set-valued predictor that controls risk with the desired high probability, specifically $$P(R[f_{\hat{\lambda}}]\leq \alpha)\geq 1-\delta.$$
By following this procedure, of selecting $\lambda$, the authors can chose holdout calibration sets that are "nearly as small as possible" depending on $\alpha$ and $\delta$ chosen by the use.


## Generalization to other risk functions
The authors extend their results to work under different notions of risk that can be used for specific  problems such as classification ranking and metric learning (related to [[Classification and clustering#Clustering|clustering]]).


# Experimental results
Five different applications are studied in the paper: Classification with loss based on the failure to predict a specific class, Multi-label classification, Hierarchical classification, Binary image segmentation, and Protein structure prediction. 

