---
layout: post
title: Day 16 in Farina's Lab - EI network
tags: [ICL Project]
include_toc: true
---

## E/I Network
- The balance of excitation and inhibition is one of the fundamental mechanisms for generating oscillations in the 
  brain.
- Excitation allows for the spreading of network activity within and outside the network. Inhibition, an opposing 
  force is required to regulate this activity. 
- The percentage of inhibitiory neurons compared to excitatory ones (i.e E/I ratio) plays a majpr role in 
  controlling the "dynamic state dynamic states, stability, and coding capabilities of neuronal networks, with the 
  resulting network activity ranging from asynchronous, irregular firing to synchronized network bursting" (Sukenik, 
  et. al 2021) 

## Shifting focus to neural population response 
Instead of looking at the activity of a single neuron, we can also consider a network of neurons and look at the 
population-level response as a whole rather than spikes of individual neurons.

> Why is this interesting now? because if I am to build a network to predict the joint angles, probably this would 
> be a population response rather than individual neuron spiking rate.

[To read](https://neuronaldynamics.epfl.ch/online/Ch12.S4.html)



### Back to the dataset: which DoFs to exclude
- A lot of back and forth to refactor the code for plotting and include it in the main
  - Looked into the data of KaJu for individual fingers
  - A whole mess with the file naming convention: was looking at a different subjects and noticed that the names are 
    different which would mess up the code