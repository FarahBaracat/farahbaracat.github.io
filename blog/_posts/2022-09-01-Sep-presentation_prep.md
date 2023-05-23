---
layout: post
title: Day 75 - Peri-Stimulus-Time Histogram
tags: [ICL Project]
include_toc: true
---

In preparation for my project progress update presentation, I am reading on ways to report the firing rate of 
neurons in an experiment. The experiment here is the finger movements and the resulting motor units change in firing 
rate.

## Peri-Stimulus-Time Histogram (PTSH)
More information can be found in [Neuronal Dynamics book, Ch7](https://neuronaldynamics.epfl.ch/online/Ch7.S2.html).
- For a repeated stimulation, the neuronal response can be resported in a PTSH with a bin width $\Delta t$.
- The idea is simply to sum the number of spikes occuring in each time bin $\Delta t$ across the different 
  repetitions, then divide by the number of repetitions and the bin width used.
- This time-dependent rate is an exmpriate estimate of the instantaneous firing rate.

<figure>
<img src="/blog/figures/PSTH.png" alt="drawing" width="100%" height="100%"/>

</figure>
