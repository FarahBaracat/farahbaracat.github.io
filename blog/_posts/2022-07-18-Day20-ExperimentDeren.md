---
layout: post
title: Day 20 in Farina's Lab - Subject in Deren's experiment 
tags: [ICL Project]
include_toc: true
---

## Setting baseline model
- Looking at scatter plots for overall firing rates: summing all the spike times from all the MUs
  - Can't see a linear relationship between the overall firing rates and the joint angle for the index which is 
    somewhat expected as I didn't consider individual MUs
- Segmenting the repetition into smaller segments and compute the firing rate of individual MUs (those are my 
  features).
  - Plot the firing rate of each MUs across the different segments of each rep. The idea is to see whether across 
    the segments of the same rep, I see somewhat a consistent firing rate. Also, this helps identify the MUs that 
    don't have any spikes across the segments. These ones should be removed either manually or by the model.





## Notes on experiment
- Quatrocento: 150 gain amplification
- 2 grids (8x8 with 10mm separation) + 1 grid (5x13 with 8mm)


