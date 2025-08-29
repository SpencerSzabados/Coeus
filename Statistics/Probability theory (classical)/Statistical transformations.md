---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - statistics
  - probability_theory
references:
---
---
# Overview
Here we are interested in techniques that allow us to gain information about functions defined in terms of a [[Fundamentals of probability theory#Random variables|random variables]]. 

# Distributions of functions of random variables 
If $X$ is a random variable with cdf $F_X(x)$, then any function of $X$, say $g(X)$, is also a random variable. Formally, if we write $Y=g(X)$, the function $g$ defines a mapping from the sample space of $X$, namely $\mathcal{X}$, to a new sample space $\mathcal{Y}$ of the random variable $Y$; that is, $g(x):\mathcal{X}\to \mathcal{Y}$, and, $g^{-1}(A)=\{x\in\mathcal{X}\mid g(x)\in A\}$.

For the random variable $Y=g(X)$ we write for any set $A\in \mathcal{Y}$, $$P(Y\in A)=P(g(X)\in A)=P(\{x\in\mathcal{X}\mid g(x)\in A\})=P(X\in g^{-1}(A)).$$Thus, defining the probability distribution of $Y$ in terms of that of $X$.

If $X$ is a discrete random variable, then $\mathcal{X}$ is countable and consequently so is the sample space of $Y$, namely $\mathcal{Y}=\{y\mid g(x)=y,\, x\in \mathcal{X}\}$. Thus, $Y$ is also a discrete random variable with pmf equal to $$f_Y(y) = P(Y=y) = \sum_{x\in g^{-1}(y)}P(X=x) = \sum_{x\in g^{-1}(y)}f_X(x),$$ for all $y\in \mathcal{Y}$.

If $X$ and $Y$ are continuous random variables, then is some cases it is possible to find _simple_ formulas for the cdf and pdf of $Y$ in terms of the cdf and pdf of $X$. The cdf of $Y=g(X)$ is $$\begin{align}  F_Y(y) &=P(Y\leq y)\\ &=P(g(X)\leq y)\\ &=P(\{x\in\mathcal{X}\mid g(x)\leq y\})\\ &=\int_{\{x\in\mathcal{X}\mid g(x)\leq y\}}f_X(x)dx. \end{align}$$Sometimes it may be difficult to identify $\{x\in\mathcal{X}\mid g(x)\leq y\}$ and carry out the above integration over the region. This is formalized in the following theorems.

It is important to track the change of samples spaces when applying transformations, such as above with $g$. It is convenient to use $\mathcal{X}=\{x\mid f_X(x)>0\}$ and $\mathcal{Y}=\{y\mid g(x)=y \text{ for some } x\in \mathcal{X}\}$. The pdf of the random variable $X$ is positive only on the set $\mathcal{X}$ and is $0$ elsewhere; this set is called the _support set_ of a distribution. Likewise, for pmfs or any non-negative function.

**Theorem:** Let $X$ be a random variable with cdf $F_X(x)$, let $Y=g(X)$, and let $\mathcal{X} = \{x\mid f_X(x)>0\}$ and $Y=\{y\mid g(x)=y\text{ for some }x\in \mathcal{X}\}$ (at shown above). Then,
  1) If $g$ is an increasing function on $\mathcal{X}$, $F_Y(y)=F_X(g^{-1}(y))$ for $y\in\mathcal{Y}$;
  2) If $g$ is a decreasing function on $\mathcal{X}$ and $X$ is a continuous random variable, $F_Y(y)=1-F_X(g^{-1}(y))$ for all $y\in\mathcal{Y}$.  

**Theorem: (Change of variable)** Let $X$ be a [[Random variables|random variable]] with pdf $f_X(x)$ and let $Y=g(X)$, where $g$ is a monotone function. Let $\mathcal{X}$ and $\mathcal{Y}$ be defined as done above. Suppose that $f_X(x)$ is continuous on $\mathcal{X}$ and that $g^{-1}(y)$ has a continuous derivative on $\mathcal{Y}$. Then the pdf of $Y$ is given by $$f_Y(y) = \begin{cases} f_X(g^{-1}(y))\left|\frac{d}{dy}g^{-1}(y)\right| & \text{ for } y\in\mathcal{Y}\\ 0 & \text{ otherwise.}\end{cases}$$See [PenState](https://online.stat.psu.edu/stat414/lesson/22/22.2). ^2e88f0

Recall for differentiable invertible functions $g$ we have $$\frac{\partial}{\partial y}g^{-1}(y) = \frac{1}{\frac{\partial g}{\partial y}(g^{-1}(y))},$$ see [Simon-Fraser-Univserity](https://www.sfu.ca/math-coursenotes/Math%20157%20Course%20Notes/sec_DerivativesofInverse.html), so the above can also be written as $$f_Y(y) = \begin{cases} f_X(g^{-1}(y))\left|\frac{1}{\frac{\partial g}{\partial y}(g^{-1}(y))}\right| & \text{ for } y\in\mathcal{Y}\\ 0 & \text{ otherwise.}\end{cases}$$

**Theorem:** Let $X$ have pdf $f_X(x)$, let $Y=g(X)$, and define the sample space $\mathcal{X} = \{x\mid f_X(x)>0\}$. Suppose there exists a partition, $A_0,A_1,\dots,A_k$, of $\mathcal{X}$ such that $P(X\in A_0)=0$ and $f_X(x)$ is continuous on each $A_i$. Further, suppose there exists functions $g_1(x),g_2(x),\dots,g_k(x)$, defined on $A_1,\dots,A_k$, respectively, that satisfy
  1) $g(x)=g_i(x)$ for $x\in A_i$;
  2) $g_i(x)$ is monotone on $A_i$;
  3) the set $\mathcal{Y}=\{y\mid g_i(x)=y \text{ for some }x\in A_i\}$ is the same for each $i=1,\dots,k$, and 
  4) $g^{-1}_i$ has a continuous derivative on $\mathcal{Y}$, for each $i=1,\dots,k$. 
  Then, $$f_Y(y) = \begin{cases}\sum_{i=1}^kf_X(g^{-1}_i(y))\left|\frac{d}{dy}g^{-1}_i(y)\right| & \text{ for }y\in \mathcal{Y}\\ 0 & \text{ otherwise.}\end{cases}$$

Before moving onto the next theorem we need to better understand the behavior of the inverted cdf, $F_X^{-1}$, of a random variable $X$. If $F_X$ is strictly increasing, then $F_X^{-1}$ is well defined; that is, $$F_X^{-1}(y) = x\Leftrightarrow F_X(x)=y.$$However, $F_X^{-1}$, as defined by the process of inversion, is not well defined in the case where $F_X$ is constant on some interval, a situation that is allowable under the [[Distribution functions of random variables#^1a548c|CDF definition]] given in [[@Casella_2001]]; whereas some books require the CDF to be strictly increasing. This problem is side stepped by instead defining the inverse cdf as below, and in either case agrees with intuition.

**Definition: (Inverse cdf or quantile function)** If $F_X$ is a cdf of a random variable $X$, then define its inverse $F_X^{-1}(y)$ for $0<y<1$ by $$F_X^{-1} = \inf\{x\mid F_X(x)\geq y\}.$$This formulation is well defined and satisfies the requirement of a cdf. ^f0ea0a

**Definition: (Probability integral transformation)** Let $X$ have continuous cdf $F_X(x)$ and define the random variable $Y=F_X(X)$. Then $Y$ is uniformly distributed on $(0,1)$, that is, $P(Y\leq y)=y$ for $0<y<1$.
_Proof:_ For $Y=F_X(X)$ we have, for $0<y<1$, $$\begin{align*}P(Y\leq y) &= P(F_X(X)\leq y)\\ &=P(F_X^{-1}(F_X(X))\leq F_X^{-1}(y)) &&\text{($F_X^{-1}$ is increasing)}\\ &=P(X\leq F_X^{-1}(y))\\ &= F_X(F_X^{-1}(y)) &&\text{(definition of $F_X$)}\\ &= y. &&\text{(continuity of $F_X$)} \end{align*}$$At the endpoints we have $P(Y\leq y)=1$ for $y\geq 1$ and $P(Y\leq y)=0$ for $y\leq 0$. All this shows that $Y$ has a uniform distribution, as required.  ^a89d65


# Linear transformations
Linear transformations are those defined linearly in terms of another (or several other) random variables. Must of the important information about these can be extracted from the above results or by properties of [[Expected values]].


# Bivariate transformations
**Theorem: (Bivariate change of variables)** Let $(X,Y)$ be a random vector with known probability distribution. Now consider a new random vector $(U,V)$ defined in terms of $U=g_1(X,Y)$ and $V=g_2(X,Y)$, where $g_1$ and $g_2$ are specified functions; i.e., $(U,V)=g(X,Y)$.

If $B\subset \mathbb{R}^2$, then $(U,V)\in B$ if and only if $(X,Y)\in A$, where $$A=\{(x,y)\mid (g_1(x,y),g_2(x,y))\in B\}.$$Moreover, $P((U,V)\in B) = P((X,Y)\in A)$, and so the probability distribution of $(U,V)$ is completely determined by the probability distribution of $(X,Y)$. Likewise, if $(X,Y)$ is a discrete random vector, where the joint pmf $f_{X,Y}(x,y)$ is nonzero on $A\subset \mathbb{R}^2$. Then $$f_{U,V}(u,v) = P(U=u, V=v) = P((X,Y)\in A_{u,v}) = \sum_{(x,y)\in A_{u,v}}f_{X,Y}(x,y)$$where $A_{u,v} = \{(x,y)\in A\mid g_1(x,y)=u\text{ and }g_2(x,y)=v\}$.

If $(X,Y)$ is a continuous random vector with joint pdf $f_{X,Y}(x,y)$, then the joint pdf of $(U,V)$ can be expressed in terms of $f_{X,Y}(x,y)$. let $A=\{(x,y)\mid f_{X,Y}>0\}$ and $B=\{(u,v)\mid u=g_1(x,y)\text{ and }v=g_2(x,y)\text{ for some }(x,y)\in A\}$. Then as noted above, the joint pdf $f_{U,V}(u,v)$ will be positive on the set $B$. Assume, the transformations $u=g_1(x,y)$ and $v=g_2(x,y)$ define a one-to-one transformation of $A$ onto $B$. This assumption allows for the equations $u=g_1(x,y)$ and $v=g_2(x,y)$ to be solved for $x$ and $y$ in terms of $u$ and $v$. Denote these inverse transformations by $x=h_1(u,v)$ and $y=h_2(u,v)$. Construct the determinate of the _Jacobian of the transformation_, $$det(J) = \begin{vmatrix}\frac{\partial x}{\partial u} & \frac{\partial x}{\partial v}\\ \frac{\partial y}{\partial u} & \frac{\partial y}{\partial v}\end{vmatrix} = \frac{\partial x}{\partial u}\frac{\partial y}{\partial v}-\frac{\partial y}{\partial u}\frac{\partial x}{\partial v},$$where $\frac{\partial x}{\partial u} = \frac{\partial h_1(u,v)}{\partial u}$, $\frac{\partial x}{\partial v} = \frac{\partial h_1(u,v)}{\partial v}$, $\frac{\partial y}{\partial u} = \frac{\partial h_2(u,v)}{\partial u}$, $\frac{\partial y}{\partial v} = \frac{\partial h_2(u,v)}{\partial v}$. Then the joint pdf of $(U,V)$ is $0$ outside the set $B$ and on the set $B$ is given by $$f_{U,V}(u,v) = |det(J)|\cdot f_{X,Y}(h_1(u,v),h_2(u,v)).$$(End of bivariate change of variables theorem.)

**Theorem:** Let $X$ and $Y$ be independent random variables. Let $g(x)$ be a function only of $x$ and $h(y)$ be a function only of $y$. Then the random variables $U=g(X)$ and $V=h(Y)$ are independent. This theorem results from applying [[Distribution functions of random variables#^89539c]].

Of course there are many transformations that are not one-to-one. Thus, to generalize the above theorem, let $A=\{(x,y)\mid f_{X,Y}(x,y)>0\}$ and suppose $A_0,A_1,\dots,A_k$ forms a partition of $A$ with the following properties:
   1) The set $A_0$ (which can be empty) satisfies $P((X,Y)\in A_0)=0$;
   2) The transformation $U=g_1(X,Y)$ and $V=g_2(X,Y)$ are one-to-one from $A_i$ to $B$ for each $i=1,2,\dots,A_k$;
   3) For each $i=1,2,\dots,k$, the inverse transformation from $B$ to $A_i$ exists. Denote each by $x=h_{1,i}(u,v)$ and $y=h_{2,i}(u,v)$. Where the $i$th inverse gives, for $(u,v)\in B$, the unique $(x,y)\in A_i$ such that $(u,v)=(g_1(x,y),g_2(x,y))$.
Let $J_i$ denote the Jacobian computed from the $i$th inverse. Then provided the Jacobians do not vanish identically on $B$, we have the joint pdf $$f_{U,V}(u,v) = \sum_{i=1}^k |det(J_i)|\cdot f_{X,Y}(h_{1,i}(u,v),h_{2,i}(u,v)).$$
