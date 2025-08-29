There exists at least two different notions of $s$-concavity for functions and sequences. The first is motivated by the study of [[Density estimation]] and [[Families of distributions]] within statics, since the concavity of a density function is important information when it comes to sampling. The second notion of $s$-convexity is a more immediate generalization of standard [[Convex functions|convexity]] and is included within the aforementioned note. The two notions are named according to the above relations in this note.

**Definition: (s-concave densities)** A sequence $\{a_i\}_{i=1}^N$ (or function $f$) with terms of the form $$a_i = \begin{cases}\phi(x)^{1/s} &\text{ for some convex function } \phi & \text{ if } s<0\\ e^{-\phi(x)} &\text{ for some convex function }\phi & \text{ if } s=0\\ \phi(x)^{1/s} &\text{ for some concave function }\phi &\text{ if } s>0\end{cases}$$is said to be $s$-concave for some fixed $s$ value. Alternatively, in terms of functions, by way of the Borell-Brascamp-Lieb inequality this can be stated as the condition $$f(\lambda x + (1-\lambda)y)\geq (\lambda f(x)^s+(1-\lambda)f(y)^s)^{1/s}$$for all $\lambda\in[0,1]$ and all $x,y$ in the domain of $f$. This definition is presented by [Wellner](https://sites.stat.washington.edu/jaw/RESEARCH/TALKS/UCL-Econ-Small.pdf).


## Log-concave densities 

^85184b

A lot of recent work has been focused on a specific subset of densities, called $\log$-concave densities, which correspond to $s=0$ in the family of $s$-concave densities.

**Lemma: (product of log-concave densities)** If $f$ and $g$ are both $\log$-concave functions (densities) then $fg$ is also $\log$-concave.
_Proof:_ This follows from the properties of logs; namely, $\log(fg)=\log(f)+\log(g)$, so if both functions are $\log$-concave then it is trivial that the product between them is also $\log$-concave.

**Lemma: (Marginals of log-concave densities)** 

