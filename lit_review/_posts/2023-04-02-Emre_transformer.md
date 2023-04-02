---
layout: post
title: Leroux, Finkbeiner and Neftci (2023) - Online transformers with spiking neurons for fast prosthetic hand control
tags: [Proportional prosthesis control]
include_toc: true
---

The paper is still under review when I read it. It can be find [here](https://arxiv.org/abs/2303.11860).
<!-- dark Orange: #ffbe76  rose:#E4D0D0  pale orange:#FFDCA9 mauve:#DEBACE  watermelon:#FF9F9F-->
## Why this paper?
This is one of the most recent papers on transformers and sEMG finger control. It also adds spiking neurons to the transformer architecture to introduce sparsity. the reported results are the highest for NinaPro DB8.


## Main Findings
- A minimum prediction <mark style="background: #FFDCA9">latency of 3.5 ms</mark>: it is the lowest reported on this dataset (Tokens are processed one at-a-time, see below for more information).
- This is achieved by exploiting local sliding windows for the transformer attention mechanism.
- The token-wise approach makes the proposed architecture implementable "online".
- Added sparsity by introducing spiking LIF neurons to replace/complement some of the transformer layers. This reduced the number of <mark style="background: #FFDCA9">MAC operations (synaptic operations) by a factor up to 5.3</mark>. 


## Background
### Transformers
- Although they are currently the state-of-the-art for sequence processing and language models, conventional transformers have an attention mecahanism that requires large time-window (i.e it needs to see the whole sequence). For online processing, this is problematic since we need the model to output predictions "ideally" at each time step.
- An added limitation of those models is the memory and computation requirements: they scale quadratically O($n^2$) with sequence length.

**Proposed method**: <mark style="background: #E9EDC9">Use local/ linearized sliding windows attention mechanism. Information from the past is stored in a "memory" as keys and values which gets updated at each token.</mark>


#### Integrating SNN in transformers
- The idea of integration spiking neurons in transformers architecture to add sparsity and hence reduce the computation requirement is not new. Some previous works:
    1. [SpikeGPT, 2023](https://arxiv.org/pdf/2302.13939.pdf) used pure binary and event-driven spiking activation units. They replaced the multi-head self attention (MHSA) with linear attention and recurrent dynamics (allowing for streaming word-by-word).
    2. [SpikFormer, 2023](https://openreview.net/pdf?id=frE4fUwz_h) proposes a spiking self-attention for visual features.
    3. [SpikeFormer, novel architecture, 2022](https://arxiv.org/pdf/2211.10686.pdf) adopts a spatio-temporal attention instead of the only spatial or only temporal attention mechanisms previously designed. Reported low latency and competittive results on DVS-CIFAR10, DVSGesture and ImageNet datasets. They also show the inmportancec of the first convolution layer to tokenize the sequence. *P.S.: The major difference between this paper and the previously mentioned is still unclear to me. I would have to go through both to spot it.*
    

## Methods
### Input/Output
- Used [NinaPro Dataset 8](http://ninapro.hevs.ch/DB8_Instructions). Contains 9 movements including both individual finger flexion/extension and combinations.
- Input: 16 sEMG channels placed on the subjects' forearm.
- Output: instead of using the 18-DoFs glove data readinds, they mapped the DoFs to 5 Degrees-of-Activation (DoA) (following the original paper of [Agamemnon Krasoulis, 2014](https://www.frontiersin.org/articles/10.3389/fnins.2019.00891/full); the rational behind the linear transformation mapping the 18 DoFs of the glove to 5 DoAs was to use a prosthesis hand with 5 DoAs: Azzura, Prensilia, hence mapping directly the output to a motor command).
- They trained <mark style="background: #DEBACE">a model per subject</mark> and reported the average accuracies and standard deviations across the different models.


### Data Augmentation
