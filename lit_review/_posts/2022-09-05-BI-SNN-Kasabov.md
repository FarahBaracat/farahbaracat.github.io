---
layout: post
title: Kumarasinghe, et al. (2021) - Brain-inspired SNN for decoding and understanding muscle activity and kinematics from EEG signals during hand movements.
tags: [Continuous prosthetic control]
include_toc: true
---


The paper can be found [here](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7844055/).

## Why this paper?
My brother found this paper and  asked me if I ever read it as it seems to be describing a similar work to mine. 
Truth be told, I never came across it before 😅 (a bit worrying but at least I know it now 🤷🏼‍♀️)

## Motivation
The main motivation for this work is to decode hand kinematics (precisely movement onset and movement trajectory) 
from EEG signals using a brain-inspired network that:
 - can learn fast
 - from few examples (i.e incremental learning)
 - while being interpretable (the trained model should help us understand the underlying cognitive processes)

## Main contribution
Integrating two models together: NeuCube (reservoir network) with the eSPANNet made it possible to "learn 
which area of the brain carry useful information for decoding a certain motor behaviour in an incremental and online 
manner"

From my side, I find the idea of perojecting the reservoir network onto an actual brain atlas interesting and exciting.

![NeuCube_eSPAN](/lit_review/figures/kasabov_2019_Neube_and_eSPAN.png)

## NeuCube
### Connectivity
This is a reservoir of spiking neurons which are pre-structure in 3D space according the brain atlas. In other 
  words, the neurons are arranged in 3D space representing areas of brain (approcx. 1cm3). These neurons are 
  initially connected with random weights using 'the small-world connectivity principle'. A small-world topology 
  refers to a network where the number of hops between two randomly chosen nodes is small compared to the number of 
  nodes in the network. This means that these networks exhibit a high global clustering coefficient (a coefficient 
  measuring the degree to which nodes in a network are clusters ) while ensuring short path length between two 
  randomly chosen nodes.  For example, in the context of social network, usually two strangers are linked by a short 
chain of common friends. In the human brian, both a structural and functional connectivity in the brain reflect 
small-world topology. 

## eSPAN Learning
In the NeuCube framework there are two phases of learning. The first is unsupervised using STDP followed by a 
supervised learning for classification and regression. Synaptic connections of the neurons in the reservoir are 
learnt using STDP. These neurons then project to readout neurons. This last layer is trained with eSPAN (Evolving Spike 
Pattern Association Neuron) described in an earlier [conference paper](https://ieeexplore.ieee.org/document/8852213/references#references) in 2019

### Idea of training eSPAN
The suggested network architecture for the eSPAN:
![eSPAN_network](/lit_review/figures/kasabov_2019_eSPAN_network.png)

- In the eSPAN topology the hidden layer is clustered as shown in the figure. Each group also called _population 
vector_ , also _SPAN 
population 
vector_*is 
connected 
to a 
single 
output neuron, and they receive input from a single input neuron.  

- In the SPAN model:
  - The weights are learnt using Widrow-Hodd/ Delta learning rule.
  - Spikes are convolved with alpha kernels to get the synaptic currents.
  - Each time there is a misclassification of the target or therer is a spike timing error between predicted train 
    and target spike train, a new neuron is added to the relevant population vector and its weights are updated 
    using the delta rule.

## eSPAN as a readout in NeuCube
Once the synaptic connections are first learnt via STDP in the NeuCube reservoir, spiking neural clusters are 
extracted and considered a SPAN population which are then trained using the same approach in the classical SPAN model.

### Network output
The output of the network is the activity of the readout layer of the SPAN populations. The output is compared to 
two signals since the objective is to predict both the movement onset and trajectory:
- Encoded EMG to spikes for the movement onset
- Encoded kinematics for the trajectory 


