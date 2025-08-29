---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - belief_functions
  - statistics
  - dempster_shafer
references:
  - https://en.wikipedia.org/wiki/Belief_propagation
  -  [[@Yager_2008]]
---
---

# Overview
Belief functions are the central working idea of Dempster-Shafer (DS) theory, which is a theory for modeling uncertainty within a fitted model based on missing data (or the credibility of supporting evidence). The Dempster-Shafer theory generalizes the [[Bayesian probability theory|Bayesian theory]] of subjective probability, which is the interpretation of Bayesian theory where probabilities correspond to a persons belief (level of confidence) in an event occurring opposed to some objective interpretation that probabilities quantify events exactly (in the model setting I see the subjective view far more when considering prior distributions).

A degree of belief (also called mass) is associated with a piece of evidence via a belief function. Probability values are then assigned to sets of possibilities rather than single events. These values are then used to construct lower and upper "probabilities" of the likelihood of an event; a probability of confidence interval.

# Fundamentals 
**Definition: (Frame of discernment or Sample space)** Let $\Theta$ be a finite set of possible answers to a question, the _frame of discernment_, then we consider the power set $2^\Theta$ as the possible answers (assuming binary states). 

**Definition: (Belief function)** A real valued function $Bel:2^\Theta\to [0,1]$ is called a _belief function_ if and only if 
  1) $Bel(\emptyset)=0$;
  2) $Bel(\Theta)=1$; and
  3) For any $n\in \mathbb{Z}_{>0}$ and subsets $A_1,A_2,\dots \subseteq A_n \Theta$ we have $$Bel\left(\bigcup_{i=1}^n A_i\right) \geq \sum_{\substack{I\subseteq \{1,2,\dots,n\}\\ I\neq \emptyset}}(-1)^{|I|+1}Bel\left(\bigcap_{i\in I}A_i\right);$$which in the case of $n=2$ reduces to $$Bel(A_1\cup A_2)\geq Bel(A_1)+Bel(A_2)-Bel(A_1\cap A_2),$$where equality holds when $A_1\cap A_2=\emptyset$ in which case belief functions reduce to probability functions. Hence, belief functions are not additive.

The key to belief functions is their limited division of belief, where as probabilities are accumulated by individual points in the frame of reference (set), belief functions allow for the assignment of probabilities to whole sets without reliance on their subdivision.

Belief function values can be further divided into parts by way of mass functions, but no further division is immediate.

**Definition: (Belief mass function)** The probability numbers that result in a belief functions value are the result of assigned mass values to subsets of $\Theta$; namely, subsets $A\subseteq \Theta$ are called _focal elements_ if $m(A)>0$ subject to the resections that $m(\emptyset)=0$ and  $$\sum_{A\subseteq \Theta}m(A)=1.$$Then, a belief function can be constructed as $$Bel(A)=\sum_{B\subseteq A}m(B).$$   ^e1a106

Importantly, the mass assignment to one subset $A$ and to another $B$ that contain some common elements need not obey any relation other than that above; this is more pronounced when we don't consider the entire power set to consists of focal elements but only a sub-collection with all others being assigned zero mass values.

On the other hand, if we are given a belief function $Bel$ we can construct a set of corresponding mass values for each $A\subseteq \Theta$ by applying the [[Mobius inversion formula]]: $$m(A) = \sum_{B\subset A}(-1)^{|A-B|}Bel(B),$$or likewise $m(\emptyset)=0$, $m(A)=Bel(A)-\sum_{B\subset A}m(B)$ using a recursive definition.

**Definition: (Belief plausibility)** Given a set $A$ in $\Theta$ define the _plausibility_ of A by $$Pl(A)=1-Bel(\bar{A}),$$as intuitively the belief attributed to the opposite of $A$ deducts from $A$'s plausibility of occurring. It follows that, $$Pl(A) = \sum_{A\cap B\neq \emptyset}m(B).$$

**Lemma: (Belief Lower and Upper probabilities)** For any subset $A$, its plausibility cannot be lower than its assumed belief; that is, $$Bel(A)\leq Pl(A).$$


# Methods of combing belief (or evidence)
When operating with beliefs and plausibilities it is important to be able to combine multiple sources of evidence into one cohesive pair for the purpose of prediction.

## Dempster's combination rule
Dempster's rule follows a three step idea: 1) Intersections are taken of the focal elements associated with the two pieces of evidence two be combined, 2) the resulting elements have their masses calculated via multiplication of their corresponding mass functions and constitute new focal elements provided their mass is nonzero, and 3) the resulting values are summed up and normalized with the removal of empty sets representing conflict in evidence.

**Definition: (Dempster's combination rule)** Given two pieces of evidence, say $e_1$ and $e_2$, for the mass of $A\subset \Theta$ over a common set of questions $\Theta$ each resented by a (independent) mass function, say $m_1$ and $m_2$ respectively can be combined (evidence) as $$(m_1\oplus m_2)(A) = \frac{\sum_{B\cap C=A}m_1(B)m_2(C)}{\sum_{B\cap C\neq\emptyset}m_1(B)m_2(C)},$$provided the denominator, _called weight of conflict_, is finite. ^58651b

The denominator (normalizer) here measures the total amount of conflict in the evidence.

**Definition: (Weight of conflict)** The weight of conflict between two sources of evidence is $$W=\log\left(\frac{1}{\sum_{B\cap C\neq \emptyset}m_1(B)m_2(C)}\right);$$Importantly, two pieces of evidence are combinable if and only if their weight of conflict is finite.

Unfortunately we cannot easily put the combination rule for belief functions into a multiplicative form as with probabilities. To work in this way, an alterative function, called the _Commonality function_, $$Q(A) = \sum_{B\supseteq A}m(B)$$can be used. For two sources of evidence $e_1$ and $e_2$ with associated belief functions (or masses) we can compute the combined commonality as$$Q(A)=\frac{Q_1(A)Q_2(A)}{\sum_{B\neq\emptyset}(-1)^{|B|+1}Q_1(B)Q_2(B)}.$$Commonality can be interpreted as representing the total amount of belief that can be moved to elements of $A$; for any two propositions $A$ and $B$ from $S$ we have $Q(A)\leq Q(B)$ and $Bel(A)\geq Bel(B)$ with $Pl(A)\geq Pl(B)$. Commonality relates to Belief in the following way, $$Bel(A) = \sum_{B\subseteq \bar{A}}(-1)^{|B|}Q(B).$$

## Conjunctive combination rule
**Definition: (Conjunctive combination rule)** Given two pieces of evidence, say $e_1$ and $e_2$, for the mass of $A\subset \Theta$ over a common set of questions $\Theta$ each resented by a (independent) mass function (or basic belief assignment), say $m_1$ and $m_2$ respectively can be combined using the _unnormalized or conjunctive combination rule_ as $$m_1\cap m_2 = m(A)=\sum_{B\cap C=A}m_1(B)m_2(C).$$This rule allows for positive masses to be assigned to the empty set, which is a violation of the close world model assumed above, as such use of this rule requires the alteration of the definition of belief as $$Bel(A) = \sum_{\substack{B\subseteq A\\ B\neq \emptyset}}m(B)$$for all $A\subset\Theta$. ^dc37a7


# Support functions and weight of evidence
Support functions allow one to weight a given piece of evidence preferentially. The mass of a set of elements is given by a corresponding set of primitive support function, each associate with a single element of the set. 

**Definition: (Simple support function)** A _simple support function_ represents a piece of evidence that provides support for a singular proposition which is a proper subset of of $\Theta$; that is, we consider only two focal elements for simple supports, the mass of the preposition and the sample set itself. Specifically, given a proposition $A$ with simple support function $f(A)=s$, where the value of $s$ is subject to the boundary condition $$f(A) = \begin{cases} 0 & \text{ if } -log(1-f(A))=0\\ 1 & \text{ if } -log(1-f(A))\to \infty \end{cases}$$which is defined in terms of the weight of support discussed below, we can state the following about a another proposition $B$ which is also a member of $\Theta$: $$m(B) = \begin{cases} s & \text{ if } B=A\\ 1-s & \text{ if } B = \Theta\\ 0 & \text{ otherwise}, \end{cases}$$and likewise, $$Bel(B) = \begin{cases} s & \text{ if } B\supseteq A\\ 1 & \text{ if } B=\Theta\\ 0 & \text{ otherwise}. \end{cases}$$
The weight of evidence maps to an evidences support in a way where two weights associated with combined evidence are likewise mapped to the resulting combination via Dempster's rule.

**Definition: (Weight of evidence)** The weight of a piece of evidence, say $e$ with support $m(A)=s$, is $w=-\log(1-s)$; thus, the weight of any piece of evidence can range from the incognisant value of $0$ to a dominating term approaching $\infty$.

**Definition: (Separable support function)** A support function is said to be separable if it is the orthogonal sum of one or more simple support functions; note, the decomposition of separable support functions into simple support functions, when working in the opposite direction, need not be unique. The total weight of evidence focused on each subset (focal element) will however remain the same.

As such, a separable support function can support multiple propositions that are proper subset of the frame of discernment; moreover, unlike for general belief functions, if $A$ and $B$ are two focal elements associated with separable support functions and $A\cap B=\emptyset$, then $A\cap B$ is also a focal element. 

**Definition: (Consonant support function)** A function $f$ is a consonant support function if and only if 
  1) $f(\emptyset)=0$;
  2) $f(\Theta)=1$; and
  3) $f(A\cap B)=\min\{f(A),f(B)\}$ for any $A,B\subseteq \Theta.$ 

Moreover, a belief function is called consonant if its focal elements are nested.

**Definition: (The total weight of evidence)** Given a set of propositions $P$, where say $A_i$ is the $i$-th proposition supported by the $i$-th component of the support of $P$ with weight $w_i$. Then the _total weight of evidence_ focused on any nonempty proper subset of $B$ of $\Theta$ is $$w(B) = \sum_{A_i=B}w_i.$$

# Making decisions using belief 
## Pignastic approach (Transferable belief model)
As mentioned in [[@Denoeux_2000]] (among other sources) decisions (rational decisions) have to be made based on a probability structure that is not susceptible to Dutch Books; that is, any method of making decisions should not continually make losing decisions regardless of the configuration of inputs, where a Dutch Book represents a configuration of probabilities (belief assignments) that would result in such decisions. Belief functions are susceptible to Dutch Books as they are not true probabilities.

Thus, to make decisions based on belief functions, they must be transformed into probability functions. The [Pignistic probability](https://en.wikipedia.org/wiki/Pignistic_probability) transformation is the only suitable transformation; the masses $m(A)$ (or set) are distributed uniformly among the elements of $A$ for all $A\in \Theta$ resulting in the following probability distribution $$BelP(x) = \sum_{\substack{A\subseteq \Omega\\x\in A}}\frac{m(A)}{|A|}. \text{ for all }x\in \Theta,$$where $\Omega$ is a collection of subsets within $\Theta$, which is the collection of singleton elements in this setting, that make up the frame of reference we are considering.

