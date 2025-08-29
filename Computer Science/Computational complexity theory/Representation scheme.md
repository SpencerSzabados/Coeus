---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - complexity_theory
---
---

# Overview
The representation size (complexity of the encoding) of a concept is an important consideration to the efficiency of a algorithm, since the time it takes to "write down" (and perform computations using the (learned - in the case of machine learning) representation is a lower bound on the running time of the algorithm.

**Definition: (Representation scheme)** A _representation scheme_ for a [[PAC-learning#^37eec5|concept class]] $C$ is a function $R:conf^*(\Sigma)\to N$, where $\Sigma$ is a finite alphabet of symbols and $conf^*(\Sigma)$ is the class of all strings composed of symbols from $\Sigma$. Any string $\sigma\in conf^*(\Sigma)$ such that $R(\sigma)=c$ is called a representation of $c$ under $R$. To capture the notion of representation size, there is associated with every $R$ a size mapping function $\|\cdot\|:conf^*(\Sigma)\to \mathbb{Z}_{\geq 0}$ that assigns a natural number size $\|h\|$ to each representation $h\in conf^*(\Sigma)$.

The most common representation scheme is using binary representations with $\Sigma=\{0,1\}$ and defining $\|\cdot\|$ to be length of the bit string. Regardless of the particulars, the size of a representation will always be within a polynomial factor of the binary string length definition. With this said, it is typically assumed the chosen representation is the most (optimal) compact. This choice provides a worst case guarantee on the performance of the algorithm over all _reasonable_ (all polynomial factor differences from optimal) representations.