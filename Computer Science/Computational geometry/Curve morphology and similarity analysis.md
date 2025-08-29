---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - computational_geometry
  - real_analysis
  - abstract_algebra
  - g
references:
---
---
# Overview
Curve morphology deals with describing the shape and characteristics of curves along with methods of comparing them.

# Measures of curve similarity
## The Frechet distance 
Informally, the frechet distance between two curves is the maximum distance a point along one of the curves has to travel as the curve is continuously deformed into the other curve.

**Definition: (Frechet distance)**  Let $f:[a,b]\to A\subset \mathbb{R}^2$ and $g:[c,d]\to A$ be two bounded plane curves. Then the Fréchet distance between them is defined as $$d_F(f,g) = \inf_{\substack{\alpha[0,1]\to[a,b]\\ \beta[0,1]\to[c,d]}}\max_{t\in[0,1]}\|f(\alpha(t))-g(\beta(t))\|,$$where $\alpha,\beta$ range over the set of continuous monotonically increasing functions from $\alpha(0)=a$ and $\beta(0)=c$ to $\alpha(1)=b$ and $\beta(1)=d$ respectively. This definition is modified version of that given by [[@Alt_1995]]. 

The Frechet distance satisfies the requirements of a [[Metric spaces#^67481a|metric]] (or _distance function_). This can be seen by considering its similarity to the supremum norm (infinity norm) between functions.

