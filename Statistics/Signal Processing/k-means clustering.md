Note [2022-09-04] : This method was placed in [signal processing] as that is the origin of the method, moreover, k-means clustering is primarily focused on vector quantization rather than [[Classification and clustering]] problems despite its utility in [[Overview of machine learning|machine learning]].

---

K-means clustering aims to partition $N$ observations into $k$ clusters (classes) by pairing observations with clusters of closest matching mean value (the cluster centres). See [Wiki](https://en.wikipedia.org/wiki/K-means_clustering). This problem is closely related to k-center clustering, with the distinction being that k-means attempts to minimize the average distance while k-centers is concerned with maximizing the distance between centres by minimizing the worst pairing.


# k-means clustering
Given a set of observations $S=\{\vec{X_1},\dots,\vec{X_N}\}$, with $\vec{X_i}=(X_{i1},\dots,X_{id})$, and a set of $k$ classes $\mathcal{C} = \{C_1,\dots,C_k\}$ each of which having an associated unknown mean value $\mu_1,\dots,\mu_k$, the goal of k-means clustering is to determine the class-observation pairings and values of $\mu_1,\dots,\mu_k$ that minimize the in-cluster variance (sum of squares distance to mean values). This can be stated more precisely by defining indicator variables $\delta_{ij}$ for each observation to indicate which of the $k$ clusters it is paired with, by having a matching nonzero coordinate value. Using this terminology, k-means seeks to find values for $\delta_{ij}$ for $i=1,\dots,N$ and $j=1,\dots,k$ and values of $\mu_1,\dots,\mu_k$ that minimize the quantity$$err(S) = \sum_{i=1}^N\sum_{j-1}^k \delta_{ij}\|\vec{X}_i-\mu_i\|^2,$$where $\mu_1,\dots,\mu_N$ are unknown; or equivalently minimize $$ \sum_{i=1}^k|C_i|Var[C_i].$$ See (p424)[[@Bishop_2006]], [Wiki](https://en.wikipedia.org/wiki/K-means_clustering).


# Algorithms 

# Applications 
# Limitations