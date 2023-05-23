---
layout: post
title: Day 23 - Simple LIF layer
tags: [ICL Project]
include_toc: true
---

## General Progress
- initial implementation of a simple LIF layer with n MU neurons, monitor states and spikes

## Questions
- Should I reset the spikes of all 250 ms windows? 
  - In other words, is each segment of 250 ms completely separate from the previous segment. I don't think this 
    makes sense. 
  - Will attempt first to run a single trial (continuously) --> what does this mean in terms of real-time 
    implementation? we would need memory? cf work by Yigit on regression