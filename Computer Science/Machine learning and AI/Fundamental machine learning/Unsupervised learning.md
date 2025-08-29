

# Problems 
## Clustering
[[Classification and clustering#Clustering|Clustering]] is a typical problem in unsupervised learning. 


## Discovering latent features 
Though data may appear high dimensional, there may be only a small number of variable features between different data points; these correspond to latent factors in the data. Focusing on such features allows us to reduce the dimensionality of the data we have to deal with, and can result in better predictive accuracy as they better capture the "essence" of each object, see [[@Murphy_2012]].

## Latent feature analysis methods 
### Principle component analysis
[[Principle component analysis]] (PCA) is a commonly used method of data dimensionality reduction. 


## Discovering graph structures 
In unsupervised learning sometimes it is beneficial to study the correlation between a set of variables (generated extrapolated from data). This data is well represented using a graph with edges linking strongly correlated variables; that is, we can learn a estimate $\hat{G}$ of the true underlying graph $G$ from that data $X$, $$\hat{G} = \arg\max P(G|X).$$Graph structures are useful for discovering hidden relations and building models used for prediction, among other applications (e.g., collaborative filtering).


