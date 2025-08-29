# Overview 
Modern [[@Tjoa_2020]] methods in artificial intelligence (AI) and [[Overview of machine learning]] (ML) have been demonstrating impressive results within many domains, and at an increasing rate. However, within some of these domains (e.g., medical, judicial, etc) there is a level of transparency and accountability required in the decision making process, a facility that many ML methods do not explicitly provide due to limitations in both design and implementation. Thus, methods of obtaining explanations for ML decisions and predictions are desired to not only justify reliability from a human perspective, but also serve as a form of accountability when errors are identified.  
$\quad$ Explainability (or interpretable) of ML algorithms have therefore unsurprisingly become a important issue in their design. Leading to developments (but yet not standardization) of interpretability assessment criteria (e.g., reliability, causality, and usability etc...) within the ML community, which serve as guilds for appropriate usage of select methods.

# Types of interpretability
There is no universal standard criteria currently used in the classification of ML interpretability, even the terminology is under contention, but nonetheless there does exist several proposed outlines for interpretability of ML algorithms [[@Velez_2017]]. 

## Perceptive interpretability
As described in [[@Tjoa_2020]] includes notions of interpretability that are _easily_ perceived by humans (e.g., highlighting portions of images used in final classification of said image). 

### Saliency 
A saliency method attempts to explain a decision by assigning _values_ to the corresponding input data in a fashion that reflects the individual _importance_ of each -- the amount any one contributes -- within the decision making process. The values need not be numeric, but should relate to the form of the input, for instance a heatmap overplayed onto an input image could serve as a collection of values for each pixel. 

#### CLass Activation Map (CAM)
#### Layer-wise Relevanec Propagation (LRP)
#### Automatic Concept-Based Explanations (ACE)

### Signal Method
