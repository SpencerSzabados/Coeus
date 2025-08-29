# Axioms of (modern) set theory
In the early twentieth century the axioms of set theory were rewritten (or formalised for the first time) to counter Russell's famous paradoxical set construction, which seemed to break the foundations of set theory at that time. In particular, here I consider Zermelo-Fraenkel set theory along with the Axiom of Choice (which was historically controversial and avoided whenever possible - however AC is now largely accepted and was found to have been implicitly used in many historical proofs etc).

**Definition: (Zermelo-Fraenkel set theory axioms)** 

The Axiom of Choice broadly states that the product between non-empty sets (perhaps infinitely many) is itself a non-empty set that can be operated on "just" like the instantiating sets, meaning we can choose elements from the resulting set in a fashion similar to that of picking elements from the originating sets. 

**Definition: (Axiom of Choice)** For every collection $\mathcal{A}$ of non-empty sets (perhaps infinite), there is a function $f:\mathcal{A}\to\bigcup\mathcal{A}$, called a _choice function_, such that, for every $B\in \mathcal{A}$, $f(B)\in B$.  

Choice functions can be thought of a mechanism that takes in a set and returns a representative element of the set which can be used to identify said set.

Note, the Axiom of Choice is not necessary to establish the existence of a choice function when $\mathcal{A}$ is finite collection of non-empty sets, or when the rule of a choice function can be stated explicitly (e.g., formulaically). The Axiom of Choice is most relevant in the construction of a choice function when the sets in question are composed of element that do not have a universal distinguishing feature among each set; e.g., picking a representative sock from infinitely many pairs where pair of socks is composed of identical socks, here we would use the axiom of choice to guarantee we can pick a random sock from each pair and such a rule works for every set.

**Theorem:** The Axiom of Choice is equivalent to the Well-Ordering principle of sets.


# Set theory laws
**Definition: (Finite DeMorgans law)** For finitely many sets $A_1,\dots,A_n$ the following are true $$\left(\bigcup_{i=1}^nA_i\right)^c = \bigcap_{i=1}^n A_i^c\quad\text{and}\quad \left(\bigcap_{i=1}^nA_i\right)^c=\bigcup_{i=1}^nA_i^c.$$