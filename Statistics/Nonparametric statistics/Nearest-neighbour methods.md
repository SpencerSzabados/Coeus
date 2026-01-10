Nearest-neighbour methods are similar to [[Parzen-Kernel density estimators]] except rather than fixing a volume and finding the appropriate values for the number of points that fall within it; instead, the number of points within a unknown volume is assumed and the appropriate volume is found.

Nearest-neighbour methods are often used in [[Classification and clustering]] (in the construction of [[Classifiers]]).

# K-nearest-neighbours
A simple and very common classification method is k-nearest-neighbour (KNN) clustering (and classification); $K$-nearest-neighbours is similar to [[k-means clustering]].

Let $\vec{X}$ be a $d$-dimensional random vector with unknown probability density $f_X(\vec{x})$ in some $d$-dimensional space $\mathcal{X}$ (e.g., Euclidean) that we wish to estimate. Suppose we are given $N$ observations in terms of random vector $\vec{X}=(\vec{x}_1,\vec{x}_2,\dots,\vec{x}_N)$. Let $V$ equal to the volume of a hypersphere $S$ centred at a point $\vec{x}$ for which we wish to estimate the probability density $f_X(\vec{x})$. Supposing $K$ of the $N$ observations have similar probability density to $\vec{x}$, that is, they belong to he same class, we grow $S$ sufficiently to encompass the first $K$ points surrounding $x$; or equivalent we can consider a fixed volume $V$ and tune $K$. The associated (required) volume then serves to calculate the estimate of the probability density,$$f_X(x)\approx \frac{K}{NV}.$$The parameter $K$ dictates the degree of smoothing between regions. 

All this effectively partitions the space into nearest-neighbour regions (average neighbour regions) based on the structure of the training data.

## Classification interpretation
An alternative way of considering $K$-nearest-neighbours is trying to learn an empirical function $\hat{f}$, as in classifying an observation $\vec{x}$ into a particular class $C$, $$P(Y=C|\vec{x},\vec{X})\approx \frac{1}{K}\sum_{\vec{x}_i\in N_K(\vec{x})}\mathbb{I}\{y_i=C\},$$where $N_K(\vec{x})$ are the $K$ nearest points to $\vec{x}$ from $\vec{X}$ under some distance measure, that estimates $f_X(\vec{x})$. Then, supposing we have $k$ classes $C_1,C_2,\dots,C_k$ we would assign $x$ to the class based on the following rule $$\hat{f}(\vec{x}) = \arg\max_{\{C_1,\dots,C_k\}}\bigg\{\frac{1}{K}\sum_{\vec{x}_i\in N_K(\vec{x})}\mathbb{I}\{y_i=C\}\bigg\},$$or equivalently $$\hat{f}(\vec{x}) = mode\{C_1,\dots,C_m \mid x\in N_K(\vec{x}) \text{ and } x\in C_i\},$$where the most common class among the $K$ nearest-neighbours of $\vec{x}$ is selected.


## Limitations
This model is not a true density as the integral over all space diverges. Additionally, in order to perform these estimates the entire set of training observations must be maintained (stored), leading to expensive computation if the data set is large. 

Furthermore, KNN based classifiers do not perform well when working on high dimensional data, since a large number of data entries need to be inspected even when we base our estimates using a few percent of the total data available. 


## Algorithms 
### Classification algorithm using $K$-nearest-neighbours 
The biggest part of running $K$-nearest-neighbours is choosing a good value for $K$. To accomplish this we partition the training data $\vec{X}$ into two parts $\vec{X}_{train}$ and $\vec{X}_{test}$ used for training the value of $K$ and subsequently testing the value of $K$ for accuracy to data outside the initial training set (generalization performance); this is done in an effort to avoid overfitting the value of $K$ to the sample data. However, in doing this we have inadvertently made $K$ dependent on the test data. Thus, we actually need to split $\vec{X}$ into three $\vec{X}_{train}$, $\vec{X}_{valid}$, and $\vec{X}_{test}$ used for training, optimizing the value of $K$, and testing generalization performance respectively. The exact partition between $\vec{X}_{train}$ and $\vec{X}_{valid}$ should be altered several times and the best performing $K$ chosen from the separate runs; [[Cross validation]].

```pseudocode
Let X[0,1,...,N] be the complete set of training data
Let K_MAX be the maximum allowed number of neighbours 
Let S be the number of splits for forming X_train and X_valid
_______________________________________________
KNN(X,K_MAX,S)
    let accuracy[K_MAX][S] be a 2D array of size K_MAX-by-S 
    for k from 1 to K_MAX do
        for s from 1 to S do
            accuracy[K] = eval(k,X_train_s,X_valid)

```