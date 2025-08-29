---
title: Set-valued prediction in hierarchical classification with constrained representation complexity
authors: Thomas Mortier, Krzysztof Dembczynski, Eyke Hüllermeier, Willem Waegeman
year: 2022
---

# Overview
The authors study the problem of [[Classification and clustering#Set-valued (multi-set) classification|set-valued classification]] with a hierarchical resection imposed on the predicative sets, where valid sets corresponds (are models) by nodes in a hierarchy tree. The idea of imposing a hierarchy on set predictions is natural, as hierarchies exist in many domains. Here the hierarchy is not learned but is assumed to be given for the set of classes considered; e.g., hierarchy provided by domain expert. For the study of this problem the authors introduce a notion of the complexity of hierarchical set predictions, and present an algorithm that run in time proportional (along with other parameters) on this complexity.

Restricting set-valued predictions to hierarchical nodes has the immediate effect of reducing prediction computational complexity for finding the best prediction as the number of possible predictions dependent on the number of nodes in the tree, which is likely to be less than the power set of all classes as typically considered in standard set-valued prediction. However such ridged predictions, which are only selected from the established hierarchy, might perform worse in comparison. To try and account for this, the authors, allow for the return of a specified number of internal nodes rather than just a single tree node.


# Primary results
Suppose we are given training data of the from $\{(X_i,Y_i)\}_{i=1}^N$ iid from an underlying distribution $P(X,Y)$ defined on $\mathcal{X}\times \mathcal{Y}$ where $\mathcal{Y}=\{C_1,\dots,C_K\}$ is a set of classes. On top of this assume a domain expert has given a tree structure $\mathcal{T}$ that contains $M$ nodes overtop of $\mathcal{Y}$, let $\mathcal{V}_\mathcal{T}=\{v_1,v_2,\dots,v_M\}$ the resulting class hierarchy with $v_i\subset\mathcal{Y}$. 

Due to the tree structure of $\mathcal{V_T}$ the probability mass of a set $v_i$ given a input $x$ can be calculated as $$P(v_i|x) = \prod_{v_j\in\text{Path}(v_i)} P(v_j|\text{Parent}(v_j),x)$$where $\text{Path}(v_j)$ is the sequence of nodes from $v_j$ to the root of the tree. For each node of the tree a multi-class probabilistic classifier (estimation of conditional probability) is trained. The authors make the assumption that such classifiers (or estimates) are given, and focus on developing a decision framework for the final output.

Let $$\mathcal{S_T}(\hat{Y}) = \left\{\hat{V}\subseteq\mathcal{V_T}\mid \bigcup_{v_i\in \hat{V}}v_i=\hat{Y}\text{ and }\bigcap_{v_i\in\hat{V}}v_i=\emptyset\right\}$$be the set of all disjoint combinations of tree nodes that represent a prediction $\hat{Y}$. Then  define $$R_\mathcal{T}(\hat{Y}) = \min_{\hat{V}\in \mathcal{S_T}(\hat{Y})}|\hat{V}|$$to be the complexity representation of prediction $\hat{Y}$. To limit representation complexity to a user specified level define the $r$-th representation complexity class of predictions as $$R_\mathcal{T}^{(r)} = \{\hat{Y}\in\mathcal{P}(\mathcal{Y}\mid R_\mathcal{T}(\hat{Y})=r\},$$which is the collection of sets that can be produced from the union nodes between $r$ disjoint branches in $\mathcal{T}$. The $r$-th representation classes form a partition of the prediction space. 

The authors then consider (optimal - in term of probability maximization) predictions of the form $$\hat{Y}^*(x) = \arg\max_{\hat{Y}\subseteq\mathcal{Y}}P(\hat{Y}|x)$$subject to the user specified constraints $$|\hat{Y}|\leq k\text{ and }R_\mathcal{T}(\hat{Y})\leq r.$$

## Algorithms
The authors present there algorithmic solutions to finding the Bayes-optimal solution to this optimization problem: a naive exhaustive method that takes $O(2^K)$ time in the worst case, a graph based algorithm (reduction to knapsack problem with conflict graph) which can be solved using a integer linear program, and lastly a recursive tree search algorithm based on the $A^*$-search that takes $O(\log_2(K^r))$ worst case time to solve the problem.


# Empirical results 
The developed method is compared against a selection of other set-valued predictors 


# Directions for future research 
Extension of the method by including set size error rates.