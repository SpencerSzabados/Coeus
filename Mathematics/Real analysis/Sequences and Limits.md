# Sequences
**Definition: (Sequence)** A _sequence_ is a function whose domain is the set of positive integers. 

If $a$ is a sequence, it is customary to write $a(n)=a_n$ for each positive integer $n$ and write $a=\{a_n\}_{n=1}^\infty$. 

**Definition: (Convex sequence)** A sequence $\{a_i\}_{i=1}^N$ is convex if it satisfies the condition $$2a_i\leq a_{i-1}+a_{i+1}$$for all $i$. Convex sequences can be both increasing and decreasing over different areas of their domain, but can only transition from decreasing to increasing and not vice versa.

**Definition: (Convergence limit)** A sequence $\{a_n\}_{n=1}^\infty$ _converges_ to a real number $A$ iff for each $\epsilon>0$ there exists a positive integer $N$ such that for all $n>N$ we have $|a_n-A|< \epsilon$.

More generally, a sequence $\{a_n\}$ of points in a metric space $(S,d)$ is said to converge to a point $A\in S$ iff for all $\epsilon>0$ these is an integer $N$ such that $d(a_n,A)< \epsilon$  whenever $n\geq N.$ 

**Theorem: (Unique limit)** If $\{a_n\}_{n=1}^\infty$ converges to $A$ and $B$, then $A=B$.

**Theorem: (Convergence bound)** if $\{a_n\}_{n=1}^\infty$ converges to $A$, then it is bounded.

# Cauchy sequences

