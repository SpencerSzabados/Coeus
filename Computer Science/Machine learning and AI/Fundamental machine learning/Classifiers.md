Machine learning classifiers are used to perform [[Classification and clustering]].

# Linear classifier
# Bayesian classifiers
Classifiers based on Bayesian probability are called Bayesian classifiers.

## Generative classifiers 
Vectors $\vec{x}$ can be classified into categories $C_1,\dots,C_k$ using a probabilistic model based on [[Bayesian probability theory|Baye's rule]] of the from $$P(Y=C|\vec{x},\theta) = \frac{P(Y=C|\theta)P(\vec{x}|Y=C,\theta)}{\sum_{C_i}P(Y=C_i|\theta)P(\vec{x}|Y=C_i,\theta)}.$$Classifiers of the form are called _generative classifiers_. [[@Murphy_2012]].

The key to using this kind of model is in specifying a suitable class-conditional density $P(\vec{x}|Y=C,\theta)$, which specifies the kind of data we expect as input.

## Discriminative classifiers 
Classifiers based on fitting the posterior probability $P(Y=C|\vec{x})$, i.e., [[Maximum posterior]], are called discriminative classifiers.