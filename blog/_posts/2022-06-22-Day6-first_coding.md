---
layout: post
title: Day 6 in Farina's Lab - Looking into Simone Dataset
tags: [ICL Project]
include_toc: true
---

- Struggling to understand how the dataset is segmented, how to extract the different gestures. I cannot really do 
  any analysis on the decomposed MUs as I don't know the start/end of the trials nor gestures.
- Emailed Simone to request kinematics dataset and setup a meeting with him on Friday
- Met with Patrick

## Patrick Meeting Minutes
**June 22**: First meeting with Patrick
- There are 2 approaches when it comes to defining what DoFs to use:
    1. Focus on only 2 grips with open/ close proportionally + wrist pronation/ supination
    2. Rely on prosthesis adaptation to the grip so don’t care much about the exact grip. The idea of grip
- He followed the second approach and used for now an open loop controller with minimal force to not squeeze in/damage the object.
* If I want to increase n DoF: add flexion/extension of wrist + ulnar/radial.
* An interesting remark he made: the reason why people are less keen to include wrist movements with simultanoeus 
  control is because of the added risk it creates. Imagine holding a cup of hot water and the network is not 
  accurate enough, then any jitter in the EMG or false predictions can lead to spilling the water. 
  * I think that it is fine in the early stages of training. If we have a model that can adapt with the user then, 
    this would be exactly how kids learn to manipulate objects with care.
* He used a <mark>linear regressive </mark> trained on only 4 reps of each DoF
* Since it’s simultaneous, can decode combination of those movements like movement in the diagonal requires both ulnar + flexion 
    * GUI used to record new data for training regression and load it for real-time control
    * Regressor trained on transient + steady state part of the signal 
    * The idea is to separate the plane so making sure there is minimal overlap in EMG channel activity
    * He custom-made the band + prosthesis hand 
* Linear regression trained on windows of 260 ms with overlap of 100 ms. Each movement is approx 1 second 
* Regarding the prosthesis: there is the [TASKA](https://www.taskaprosthetics.com) hand, Softhand, MichelAngelo and his prototype.


### TASKA vs. SoftHand vs. MichelAngelo
- TASKA: wrist can be locked in 3 positions, so I assume there is no proportional control on the wrist.
- MichelAngelo: 
  - wrist moves. 
  - Thumb/index and middle are controlled separately while ring and little finger follow 
    the rest. 
  - No adaptive grip


