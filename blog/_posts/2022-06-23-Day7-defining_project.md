---
layout: post
title: Day 7 in Farina's Lab - Towards a more concrete definition of the project
tags: [ICL Project]
include_toc: true
---

- Been reading about grip force regulation in prosthesis and came across an [interesting note](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6190905/): 
> Most upper-limb amputations are below elbow, and a greater percentage of people with amputations use body powered artificial limbs, as opposed to externally powered prostheses such as myoelectrically controlled devices.

- Simone provided the dataset and we are meeting tomorrow anyways to go through it.

## Some questions regarding SNN + MUs
- MUs discharge timings already match the force profile. So if we have a network that can reproduce that with more 
  stability...would that solve the problem already?
  - Maybe not since the idea is in the separability of the different grasps or grasp positions from those input 
    spike trains.
  - A network is not required if the problem is linearly separable already (would a linear regressor solve the task?)