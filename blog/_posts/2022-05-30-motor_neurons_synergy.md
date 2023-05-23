---
layout: post
title: Synergistic Organization of Motor neurons and Hand Muscles
tags: [CapoCaccia 22 Project]
include_toc: true
---

I wanted to understand how motor units activity control individual hand fingers. **How does this happen?**

I came across a paper by Simone Tanzerella and Dario Farina from last year exploring motor neurons synergies. I find 
it interesting...The hypothesis is that people have been concerned with muscle synergies, we (the authors not me... 
I wish 😅) will 
attempt to 
focus 
on motor neurons to test whether they as well follow a synergistic organization. 

The idea is stemming from the fact 
that the number of motor neurons is much larger than the muscles they innervate. It follows that there must be some 
dimensionality reduction taking place at the level of the motor neurons output. It was further hypothesized that 
this dimensionality reduction happens because of **the presence of a common synaptic input**.

---

## Study Methods
- They identify motor neuron synergies and muscle synergies independently. This is done by:
  1. Decomposition into motor neurons using Convolution Kernel Compensation (CKC)
  2. Apply Non-negative Matrix Factorization (NMF) once for the decomposed motor neurons and another time for the 
     EMG envelopes.
     - For the motor neurons, they first get a smoothed discharge rates (SDR) which are claimed to represent the 
       instantaneous firing rates for each motor unit.
     - They call *motor neuron synergies* the resulting **time-invariant** weight matrix from SDR and *muscle 
       synergies* the weights identified from EMG envelopes.


### What is NMF?
Here is a [nice blog](https://blog.acolyer.org/2019/02/18/the-why-and-how-of-nonnegative-matrix-factorization/) 
briefly explaining NMF.
- It is a commonly used technique to reduce a high dimensional data into a set of lower dimension sparse features.
- Given an input matrix X, with dimensions  p x n (where p is the number of dimensions and n is the number of 
  datapoints). For EMG signal for example, p would be the channels and n is the time step. For the case of motor 
  neurons, p would be the motor neurons and n columns represent the time samples. 
- NMF tries to find two 
  matrices W (p x r)  and H (r x n) such that:

  $X \approx W. H$

- Interpretation of W: each column is a *basis element* (i.e a feature that is affecting all the n data points) so W 
  has the same p dimensions by only r *basis* columns. 
- Interpretation H: this is the linear combination of the basis elements of  W to reconstruct X. 

- So how do we get those matrices W and H? Simply by trying to minimize some distance measure between the original 
  matrix X and the reconstruction W.H .

<img src="/blog/figures/NMF_X.png" alt="drawing" width="420"/>

<img src="/blog/figures/NMF_X_W_H.png" alt="drawing" width="420"/>

## What can we do now with these motor neurons and muscle synergies?
- Findings in this paper show that motor neuron synergies provide a greater correlation with force than muscle 
  synergies.
- Motor neuron synergies (identified weights) functionally explain better
- Although comparable number of synergies was identified for motor neurons and EMG, yet motor neuron synergies are 
  more "robust" since the SDR are cross-talk free unlike EMG channels.
- Motor neurons appear to be controlled in clusters, i.e motor neurons innervating the same muscle were activated 
  within the same synergy. This finding goes in line with the low-dimensionality of the common synaptic input that 
  the motor neurons receive.
  > In fact, motor neurons may receive input from different interneurons whose activity is modulated in common, possibly because such interneurons receive a common input or because of other complex network dynamics. Our approach allows us to interpret the activation signals of each synergy as the common input to the corresponding group of motor neurons for each task condition.