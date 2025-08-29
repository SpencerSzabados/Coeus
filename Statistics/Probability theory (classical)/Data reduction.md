Given a sample $X_1,\dots,X_N$ for which we wish to make inferences about an unknown parameter $\theta$. If the sample size is large, then the observed sample $x_1,\dots,x_N$ may be hard to interpret without summarization.

Any [[Random samples#^1176b9|statistic]], $T(\vec{X})$, defines a form of data reduction or data summary. Data reduction in terms of a particular statistic can be thought of as a partition of the sample space $\mathcal{X}$. Let $\mathcal{T} = \{t\mid t=T(\vec{x}) \text{ for some }\vec{x}\in \mathcal{X}\}$ be the image of $\mathcal{X}$ under $T(\vec{x})$. Then $T(\vec{x})$ partitions the sample space into sets $A_t=\{\vec{x}\mid T(\vec{x})=t\}$ for some $t\in \mathcal{T}\}$. The statistics summarizes the data by reporting $T(\vec{x})=t$.

# The sufficiency principle 
A _sufficient statistic_ for a parameter $\theta$ is a statistic that captures all the information about $\theta$ contained in a sample.

**The sufficiency principle:** If $T(\vec{X})$ is a sufficient statistic for $\theta$, then any inference about $\theta$ should depend on the sample $\vec{X}$ only thought the value $T(\vec{X})$; that is, if $\vec{x}$ any $\vec{y}$ are two sample points such that $T(\vec{x})=T(\vec{y})$, the the inference about $\theta$ should be the same whether $\vec{X}=\vec{x}$ or $\vec{X}=\vec{y}$ is observed.

## Sufficient statistics
**Definition: (Sufficient statistic)** A statistic $T(\vec{X})$ is a _sufficient statistic_ for $\theta$ if the conditional probability distribution of the sample $\vec{X}$ given the value of $T(\vec{X})$ does not depend on $\theta$. ^576682

**Example:** This can be nicely exemplified using the following situation: Consider Experimenter.1, who observes $\vec{X}=\vec{x}$ and, of course, can compute $T(\vec{X})=T(\vec{x})$. To make an inference about $\theta$ they could use the sample information of $\vec{X}=\vec{x}$ and $T(\vec{X})=T(\vec{x})$. Now consider Experimenter.2, who is not given $\vec{x}$ but only that $T(\vec{X})=T(\vec{x})$. Experimenter.2 knows $P(\vec{X}=\vec{y}|T(\vec{X}=T(\vec{x})))$ for some unknown $\vec{y}$, is a probability distribution on $A_{T(\vec{x}))} = \{\vec{y}\mid T(\vec{y}=T(\vec{x})\}$. Thus, Experiemtner.2 can use this distribution to generate a random sample $\vec{Y}$ that satisfies $P(\vec{Y}=\vec{y}\mid T(\vec{X})=T(\vec{x}))=P(\vec{X}=\vec{x}\mid T(\vec{X})=T(\vec{x}))$. Note that both events $\{\vec{X}=\vec{x}\}$ and $\{\vec{Y}=\vec{x}\}$ are subsets of the event $\{T(\vec{X})=T(\vec{x})\}$. Then, we have $$\begin{align}P_\theta(\vec{X}=\vec{x})&= P(\vec{X}=\vec{x}|T(\vec{X})\\ &=P(\vec{X}=\vec{x}|T(\vec{X})=T(\vec{x}))P_\theta(T(\vec{X})=T(\vec{x}))\\ &=P(\vec{Y}=\vec{x}|T(\vec{X})=T(\vec{x}))P_\theta(T(\vec{X})=T(\vec{x}))\\ &=P_\theta(\vec{Y}=\vec{x}).\end{align}$$Meaning $\vec{X}$ and $\vec{Y}$ have the same unconditional probability distribution. Consequently, it turns out that Experimenter.1 and Experimenter.2 both have the same knowledge of $\theta$, despite Experimenter.2 not knowing $\vec{X}=\vec{x}$. This is what it mean for a statistic to be sufficient. However, an Experimenter who calculates only sufficient statistics and later ignores the rest of the data may be placing strong faith in the assumptions of the data's model/distribution if it were not known beforehand.

**Theorem:** If $p(\vec{x}|\theta)$ is the joint pdf (of pmf) of $\vec{X}$ and $q(t|\theta)$ is the pdf (or pmf) of $T(\vec{X})$, then $T(\vec{X})$ is a sufficient statistics for $\theta$, if for every $\vec{x}$ in the sample space the ratio  $p(\vec{x}|\theta)/q(T(\vec{x}|\theta)$ is constant as a function of $\theta$ (does not depend on $\theta$).

Constructing a sufficient statistic from the definition is impractical, as we must first guess as to a possible from and then test it's properties. The next theorem allows us to more easily determine sufficient statistics.

**Theorem: (Factorization theorem by Halmos and Savage)** Let $f(\vec{x}|\theta)$ denote the joint pdf (or pmf) of a sample $\vec{X}$. A _statistic_ $T(\vec{X})$ is _sufficient_ for $\theta$ is and only if there exists functions $g(t|\theta)$ and $h(\vec{x})$ such that, for all sample points $\vec{x}$ and all parameter points $\theta$, $$f(\vec{x}|\theta) = g(T(\vec{x})|\theta)h(\vec{x}).$$
### Minimal sufficient statistics 
For any problem there are many sufficient statistics. 

**Definition: (Minimal statistics)** A sufficient statistic $T(\vec{X})$ is called a _minimal sufficient statistic_ if, for any sufficient statistic $T'(\vec{X})$, $T(\vec{x})$ is a function of $T'(\vec{x})$.

Minimal statistics are not unique; any one-to-one function of a minimal sufficient statistic is also a minimal sufficient statistic.

Saying $T(\vec{x})$ is a function of $T'(\vec{x})$ means, if $T'(\vec{x})=T'(\vec{y})$ then $T(\vec{x})=T(\vec{y})$.

## Ancillary statistics 
**Definition: (Ancillary statistic)** A statistic $S(\vec{X})$ is called an _ancillary statistic_ if it's distribution does not depend on the parameter $\theta$.

Paradoxically, an ancillary statistic, when use in conjunction with other statistics, sometimes contains information for inferences about $\theta$.


# The likelihood principle 
An important statistic called the likelihood function (e.g., [[Maximum likelihood]]) can be used to summarize data.

**Definition: (Likelihood function)** let $f(x|\theta)$ denote the joint pdf (or pmf) of the sample $\vec{X} = (X_1,X_2,\dots,X_N)$. Then, given that $\vec{X}=\vec{x}$ is observed, the function of $\theta$ defined by $$L(\theta|\vec{x}) = f(\vec{x}|\theta)$$is called the likelihood function. 

If $\vec{X}$ is a discrete random vector, then $L(\theta|\vec{X})=P(\vec{X}=\vec{x})$. Comparing the values of the likelihood function at two parameter points $$P_{\theta_1}(\vec{X}=\vec{x}) = L(\theta_1|\vec{x}) > L(\theta_2|\vec{x}) = P_{\theta_2}(\vec{X}=\vec{x}),$$then the sample we observed is more likely to have occurred if $\theta=\theta_1$ than if $\theta=\theta_2$. Alternatively, if $\vec{X}$ is a continuous real-valued random vector and if the pdf of $\vec{X}$ is continuous in $x$, then, for small $\epsilon$, $$\frac{P_{\theta_1}(\vec{x}-\epsilon<\vec{X}<\vec{x})}{P_{\theta_2}(\vec{x}-\epsilon<\vec{X}<\vec{x})} \approx \frac{L(\theta_1|\vec{x})}{L(\theta_2|\vec{x})},$$and comparison of likelihood at two parameter values gives an approximate comparison of probability of the observation of the observed sample.

Hence, parameter values that maximize the likelihood for a given observation can be interpreted as being more plausible.

**Likelihood principle:** If $\vec{x}$ and $\vec{y}$ are two sample points such that $L(\theta|\vec{x})$ is proportional to $L(\theta|\vec{y})$, that is, there exists a constant $c(\vec{x},\vec{y})$, constant with respect to fixed values of $\vec{x}$ and $\vec{y}$, such that $$L(\theta|\vec{x}) = c(\vec{x},\vec{y})L(\theta|\vec{y})\quad \text{for all $\theta$},$$then the conclusions drawn from $\vec{x}$ and $\vec{y}$ should be identical. More formally, consider an experiment $E=(\vec{X},\theta,f(\vec{x}|\theta))$ and suppose $T(\vec{X})$ is a sufficient statistic for $\theta$. If $\vec{x}$ and $\vec{y}$ are sample points satisfying $T(\vec{x})=T(\vec{y})$, then the evidence about $\theta$ drawn from $E$ for $\vec{x}$ and $\vec{y}$ is the same. 

The likelihood principle can be derived from the sufficiency principle in combination with the following conditionality principle, as shown by Birnbaum's Theorem.

**Conditionality principle (Informal):** Given two experiments that share the same unknown parameter $\theta$, if one of the two experiments is randomly chosen to be performed, yielding data $\vec{x}$, the information about $\theta$ _depends only on the experiment performed_. That is, it is the same information as would been obtained if it where decided (nonrandomly) to do that experiment from the beginning, and data $\vec{x}$ had been observed. The fact that this particular experiment was performed, rather than some other, has not increased, decreased, or changed knowledge of $\theta$.


# The equivariance principle 
In any application of the equivariance principle, a function $T(\vec{x})$ is specified, but if $T(\vec{x})=T(\vec{y})$, then the equivariance principle states that the inference made if $\vec{x}$ is observed should have a _certain relationship_ to the inference made if $\vec{y}$ was observed, although the two inferences may not be the same.