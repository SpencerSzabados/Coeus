A key difference between feature representation in deep learning versus classical machine learning [[Knowledge representation and features]] is that each layer in the chain of transforms applied to the original data (use to extract features), $$\vec{x}_{l+1} = \Phi(A_l\vec{x}_l+\vec{b}_l)\quad\text{for layer $l$},$$have no fixed parameters, instead these parameters are themselves optimization variables.  Thus, the knowledge representation is encoded into the various connections and parameters between layers of model.


# Standard network (layer) forms
There are serval established standard forms these layers are sculpted into. The particular feature presentation, or rather layer configuration, chosen is typically cased the _model architecture_ in the context of deep learning.


## Fully connected layers
Fully connected layers are unstructured [[Artificial neural networks#Classical Neural networks|classical neural networks]]; i.e., for a (fixed - layer dependent) nonlinear function $\sigma$, a feature vector (raw data) $\vec{x}$ is taken to $\vec{z}$ by $$z_i = \sigma\left(\sum_j A_{ij}x_j+b_i\right).$$
There is little or no gain in approximation power by concatenating fully connected layers compared to using a single such layer, per [Amit Daniely 2016]. 


## Convolutions 
[[Knowledge representation and features#Convolution methods|convolutions]] are one of the most important methods in deep learning. The number of parameters used in defining a [[Convolutional neural networks|convolutional layer]] is much lower than a fully connected layer.

The linear map of a convolution can be expressed for a (fixed - layer dependent) nonlinear function $\sigma$, as$$z_{a,b,c} = \sigma\left(\sum_{i,j,k} A_{i,j,k,c}x_{a-i,b-j,k}+b_c\right).$$where a feature vector (raw data) $\vec{x}$ is taken to $\vec{z}$.


## Recurrent structures
Recurrent structures capture repeatable stationary patterns in time and space domains, where each such layer is a static function of the previous. When these functions are written as a neural networks, they are called [[Recurrent neural networks]].







