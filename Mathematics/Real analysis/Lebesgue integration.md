Lebesgue integration extends the notions [[Riemann-Stieltjes Integrals]] (and likewise [[Riemann integration]]) to include more notions of measurability and as such is more dependent on notions of [[Measure spaces]] or measure theory than the former. The Lebesgue integral is better suited at dealing with the limiting behaviour of sequences of functions compared to the Riemann-Stieltjes integral.

# Overview
**Definition: (Lebesgue measure)** For an interval $I=[a,b]$ let $\mathcal{l}(I)=b-a$ denote its [[Rectifiable curves and arc length|length]]. Then for any subset $S\subset \mathbb{R}$, the Lebesgue outer measure $\lambda(S)$ is defined as $$\lambda(S) = \inf\left\{\sum_{i=1}^\infty \mathcal{l}(I_i)\mid \{I_i\}_{i\in\mathbb{N}} \text{ is a sequence of open intervals with } S\subset\bigcup_{i=1}^\infty I_i\right\};$$that is, $\{I_i\}_{i\in \mathbb{N}}$ is a open cover of $S$. More generally, we can consider $S$ to be any subset of $\mathbb{R}$, if it is bounded then it will have finite measure, if it is unbounded its measure is said to tend to infinity. See [[@Schervish_1995]]. ^c700cf

**Properties:** For any $A,B\subseteq \mathbb{R}$ with $A\cap B=\emptyset$, $\lambda(A\cup B)=\lambda(A)+\lambda(B)$.


