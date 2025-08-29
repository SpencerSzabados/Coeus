---
doc type: Note
authors: Spencer Szabados
date: 
tags:
  - machine_learning
  - classification
  - statistical_learning
  - belief_functions
  - dempster_shafer
references:
---
---
# Overview
Dempster-Shafer theory has been applied to problems in [[Classification and clustering]] within machine learning, particularly for supervised learning problems where one seeks to combine various sources of information with the goal of deriving a output with lower uncertainty than would otherwise be achieved by using only a single source of information.

According to [[@Tong_2021]] there are three main methods being used for performing classification using DS theory: 
1) _Classifier Fusion_: where outputs of several different classifiers are transformed into [[Belief functions]] and then combined (using a chosen combination rule) to yield the final classification output; 
2) _Evidential Calibration_: where decision of several classifiers are converted into [[Belief functions#^e1a106|mass functions]] with "some frequency calibration property";
3) _Evidential Classifiers_: in which evidence is based directly on input features by transforming said input features into mass functions that are then combined using [[Belief functions#^58651b|Dempster's Combination rule]]; one method of transforming features into evidence is to consider a measure of distance between a given input to various vector prototypes. The combined masses can then be used to perform classification using a variety of methods to select the appropriate class (or collection of classes for set-valued classification)

# Classifier fusion methods 
Classifier fusion refers to method of combining output of various classifiers via belief function transformations into a single output value with, ideally, lower uncertainty than that of the constituent classifiers (or inputs) on their own; see [[@Tong_2021]], [[@Ma_2021]] [[@Bi_2012]]

# Evidential calibration 
See [[@Bates_2021]] (not based on DS theory but based on calibration of classifier values after training), 
