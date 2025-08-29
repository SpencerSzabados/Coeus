---
doc type: Note
authors: Spencer Szabados
tags:
  - generative_models
  - machine_learning
  - summary
---
___

Generative models have a lot of overlap with [[Overview of probabilistic learning|probabilistic learning]] methods, with the difference between the two being in their application, with generative models primarily being used for generating new samples (e.g,. images of people) where probabilistic learning methods are used to construct robust methods that can offer theoretical guarantees on certain aspects of their performance; however, there still exists many methods within the category of generative models that are entirely empirically driven in their construction. Generative modeling can be either a [[Unsupervised learning]] problem or [[Supervised learning]] problem. 


# Overview 
Generative models can be broken broadly into the following categories, with most models attempting to approximate the [[Push-forwards models#^599c6e|push-forwards measure]]. 

+ [[Push-forwards models]]
     + [[Variational autoencoder]]
     + [[Generative adversarial networks]]
     + [[Normalizing flows]] (or more generally neural flows)
     + [[Diffusion models]]

+ Graphical models 
    + [[Sum-product networks]]
