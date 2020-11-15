---
layout: post
title: Unusual Things in Machine Learning and Data Science (Running list)
tags: [ml, machine-learning, list]
---
Every now and then, I stumble across unusual, contradictory, or just plain 'that can't be right' results in my work, and I never really document them. I'd like to change that! This is a running list of things that meet my own criteria for strangeness. Many of these may have perfectly reasonable explanations and/or would be obvious to others, but I personally found them to be unintuitive. 

1. Platt-scaled non-LR models may yield MUCH better calibration results compared to an LR model, even when the accuracies of the two are identical. (11/5/2020)
  * More specifically, lets say you have two classifiers: a gradient-boosted tree and a logistic-regression. The former obviously gives poorly calibrated results, the latter (is supposed) to give well-calibrated results. And lets say that, because we have a relatively simple dataset, the metrics between the two are identical. However, if you platt-scale the gradient boosted tree, what you may find is massively better calibration compared to the logistic-regression. Personally, I would've expected nearly identical calibration results given that the metrics between the two are the same. 
  
  
2. Emebedding layers are mathmatically identical to one-hot encoding categorical inputs + dense layers. The only difference is in computational/memory expense. (11/5/2020)
  * [Here's a more in-depth explanation](https://stackoverflow.com/questions/47868265/what-is-the-difference-between-an-embedding-layer-and-a-dense-layer). Obvious after thinking a bit about it, but I always assumed there was something extra going on in the embedding layers. 
  
 
3. Using shallow copies of lists in a Spark UDF's *will* lead to nondeterministic behavior that is extremely difficult to track down. (11/5/2020)
  * So, we all know that doing `[[]] * 5` in Python will lead to five nested lists that all belong to the same memory address, but at least I sometimes forget that, write it anyway, and discover the bug via all the sublists being the same in the utput. Harmless little bug that is easy to find. However, if you use this code in a Spark UDF, whatever distributed computing magic it's doing under the hood makes the ouput look *insane*. Like, rows containing data from other rows insane. I once spent 3 weeks trying to find out what exactly was going on before a very helpful engineer pointed out that it may be a memory address issue. 
