---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - complexity_theory
references:
---
---

# Overview
A core aspect of performing time complexity comparisons ([[Reductions#^fae59d|Karp reductions]]) is devising a fixed [[Representation scheme|encoding]] scheme for the problem and algorithm that can be reduced to another problem. Unless otherwise stated, the $RAM-WORD$ model is assumed.

**Definition: (Decision problem)** A _decision problem_ (of a more general problem) is a problem that can be posed as a yes-no question based on the input values.

# Decision problem classes
Most problems admit a decision version, which is to say most problems can be rephrased into a sequence of decision problems where the difficulty of solving the decision problem is at most a polynomial factor away from solving the original question.

**Definition: (Class $TIME(f(n))$ problems)** The class $TIME(f(n))$ contains all problems for which a deterministic algorithm exists capable of solving any instance of size $n$ in time $O(f(n))$.

**Definition: (Class of $P$ problems)** The class $P$ contains all problems for which there exists a algorithm that solves any instance of the problem of size $n$ in $O(n^k)$ time for some constant $k$; that is, $P=\cup_{k\geq 0}TIME(n^k)$. Problems within $P$ are referred to as _tractable_.

**Definition: (Class of $NP$ problems)** The class $NP$ contains all decision problems where a solution to a problem instance can be verified in polynomial time; more precisely, a problem $A$ is in $NP$ if there exists a polynomial $p$ and a verification algorithm $V(I,x)$ satisfying:
  1) If $I$ is a yes-instance of $A$, then there exists an $x$ of length at most $p(|I|)$ with $V(I,x)=1$;
  2) If $I$ is a no-instance of $A$, then for every $x$, $V(I,x)=0$.

The probable solution $x$ is known as a _witness_ (or _certificate_ or _proof_) of problem instance $I$. It can generally be assumed that $x$ and $I$ are given using binary encoding. Importantly, a while yes-instance of problems in $NP$ have short proofs, this does not imply no-instances will have short proofs (or long ones either).

**Theorem: (P is a subset of NP)** The class $P$ is contained within $NP$.

**Definition: (Class of $EXP$ Problems)** Let $EXP$ denote the class of problems that can be solved in exponential time; that is, $EXP=\cup_{k>1}TIME(2^{n^k})$. 

**Theorem: (NP is a subset of EXP)** The classes are arranged $P\subseteq NP\subseteq EXP$.

**Definition: (Class of $NP-complete$ problems)** A decision problem $A$ is $NP-complete$ if the following conditions are obeyed:
  1) $A\in NP$, and 
  2) For all $B\in NP$ it can be shown $B\leq_p A$.
If a decision problem $A$ satisfies condition (2) but not necessarily (1), the problem is called $NP-hard$.

Thus, any $NP-complete$ problem is said to be as hard as any other. Verification of all possible [[Reductions]] is cumbersome, thankfully there is a easier sufficient condition.

**Lemma:** Suppose $A$ and $B$ are decision problems with $B\leq_p A$, and $A\in NP$ and $B\in NP-complete$. Then $A\in NP-complete$.

Thus, it is enough to show there exists a single reduction from a known $NP-complete$ problem to the one you are attempting to prove to be $NP-complete$.


