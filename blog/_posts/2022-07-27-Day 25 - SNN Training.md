---
layout: post
title: Day 25 - Heterogeneity and synaptic weight training
tags: [ICL Project]
include_toc: true
---

## General Progress
- Plumbing to add the grips as well

## Notes
- The wrist is a categorical data. This means that for simultaneous control, I would regress on the individual 
  fingers but classify the wrist state (flexion/extension)
- An alternative or complementary model would be to train/fit on individual fingers and validate on the grips data.


## Questions
- Do I need to train the synaptic weights or adding random distribution on the parameters sufficient?
- Can we fit different regressor models (one per finger) and use that to predict the grips?
- Is a leaky integrator model the same as LIF neuron with very high v_thr?
  - Does it even matter if the neuron is spiking or not, I can still look at Iin instead of v_mem
- Floating-point precision vs limited synaptic weight resolution?
- Again, is there any limitation on the duration of the input stimulus? (ex. for Dynapse in the loop)