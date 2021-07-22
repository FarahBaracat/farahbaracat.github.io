---
layout: post
title: Xu, Zheng and Hu (2021) - Estimation of Joint Kinematics and Fingertip Forces using Motorneuron Firing Activities. A Preliminary Report 
tags: [Continuous prosthetic control]
include_toc: true
---
The paper can be found [here](https://ieeexplore.ieee.org/document/9441433).


## Why am I reading this conference paper?
To better understand how they combine decomposition techniques (i.e motorneuron firing patterns) to design a continuous controller.

---
## Motivation
There are two main approaches to drive robotic devices: 
1. **Pattern recognition approaches**: classification-based, are limited to discrete states of user intent.
2. **Continuous approaches**: regression-based (ex. linear or quadratic regressor), are used to "continuously" estimate joint kinematics and forces (for instance). The problem with these approaches in the context of EMG is that they are unstable over time. They rely on the amplitude of the EMG signals as input features which deteriorate over time (due to amplitude drift and electrode shift).

This motivates the use of motor unit action potentials (MUAPs) to estimate the neural drive instead of relying on the EMG signals (given that EMG signals "intrinsically comprise MUAPs"). MUAPs therefore provide a more stable basis for regression. Once the separation matrix is learnt, it can be directly applied to new HD-EMG signals.

---
## Main Contribution
The method for MU decomposition, validation and estimation of a finger joint angle in a dynamic task and force in an isometric task.
The novelty here is, to my opinion 😀, in the MUs cross-trials validation on a preliminary study (validating the obtained MUs on a second trial before actually testing them).

---
## Methods
- 3 healthy participants
- HD-EMG data acquired: 8x16 electrode array. Signals sampled at 2048 Hz and bandpassed 10-900 Hz
  - Load cell used to record the finger forces and angle sensors for joint angles recordings.
- 2 tasks were performed: isometric finger flexion force (index and middle finger) and dynamic finger movement task (flex and release repetitively)

### MU identification
- Decomposition used is based on the **Fast independent component analysis (FastICA)**. 
- The algorithm is carried **offline**. The goal of the decomposition is to separate or resolve the superimposed (spatiotemporally) MUAPs into individual MU activities. This is achieved through the following steps:
  1. Extending the raw signal ( by adding R delayed replicas of the original signals in each channel)
  2. Whitening the extended channels
  3. Getting the decomposed signal sources using a fixed-point iteration algorithm. This step leads to the separation vectors. 
  4. Multiplying the EMG with the separation matrix to obtain the decomposed source signals (MUs spike trains).
  
### MU validation
To validate the decomposition, the separation matrix is computed/derived from a trial and then applied on a second trial before being used on a third testing trial:

  - By applying the separation matrix on the second trial, they obtain a spike array of $M_i$ X $K_j$; M is the length of the EMG in the second trial and K is the number of decomposed MUs from the first trial.
  - Run a regression analysis between the firing frequency of the spike trains and the measured joint angle/isometric force. The output of this analysis is  $K_j$ $R^2$ values; how well each MU obtained on the first trial estimates the motor task on the validation trial.
  - Retain the top 10 MUs with the strongest association to the motor task.

---
## Results
- Estimation joint angle and isometric force from neural drive (MUs) is more accurate than EMG amplitude. It showed a smaller RMSE.
- For joint angle estimation, EMG amplitude error is around **20 degrees** compared to **8 degrees** for the MU approach during dynamic movement.
![neural_drive_results](/blog/figures/Hu_neuraldrive_vs_amp.png)
![neural_drive_MU](/blog/figures/Hu_MUs_neural_drive.png)
  
---
## Limitations 
 - The decomposition is computationally intensive and is not therefore practical in real-time. However, a solution would be to obtain the MUs offline in an initialization period then use the separation matrix in real-time. The underlying assumption is that a common set of MUs is recruited across different muscle activations (i.e. MUs form a common input to the muscles).
  
 - The decomposition was performed separately for each task. Is it feasible to estimate the neural drive (MU firing frequency) directly using neural network approaches? Interesting examples of ANN approaches for a generic decomposition to look at:
   - Paper by Farina et al., *Deep Learning For Robust Decomposition of High-Density Surface EMG Signals*, (2020). 
   - Paper by Hu et al. *Real-time finger force prediction via parallel convolutional neural networks: a preliminary study*, (2020). 

---
## Final Thoughts
- Overall, I think it is a nice paper. I didn't get yet why choosing ICA in the first place as opposed to other decomposition techniques, but I guess this is related to their earlier paper on *Independent Component Analysis Based Algorithms for High-Density EMG Decomposition, Dai & Hu (2019)*.

- One minor comment on the decomposition of EMG for the dynamic task: as the authors stated, extracting the MUs is challenging for the dynamic task, but why is this the case?

