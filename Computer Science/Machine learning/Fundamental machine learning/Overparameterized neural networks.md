Overparameterization of a model refers _roughly_ to models that include more parameters than data points in their training sets. However, the term also get used when simply referring to models with a _large_ number of parameters (a large number of hidden layers and weights). In practice [2022] overparametrized models are both easier to train and suffer less from overfitting. The theoretical reasoning for this is not generally known, but it is speculated that the used of a large number of (randomly initialized) parameters increases the _apparent_ convexity of the systems leading to quicker training, [[@Fang_2021]].

https://dsgissin.github.io/blog/2019/07/01/canonical_spaces_1.html

## Methods of analysis
### Neural tangent kernel (NTK)
