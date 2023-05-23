---
layout: post
title: Notes on Ninapro database, muscle synergies, MEMS
tags: [CapoCaccia 22 Project Prep]
include_toc: true
---

## Ninapro Database
- There are 10 datasets in NinaPro. Since the goal of my project is to estimate finger position as opposed to 
grip/grasp. 
[Database 8](http://ninaweb.hevs.ch/DB8_Instructions) 
seems very suitable for the task. 
- The paper describing this dataset can be found [here](https://www.frontiersin.org/articles/10.3389/fnins.019.
  00891/full). DB 8  as the documentation clearly suggest should be used for regression 
problem and not 
classification. "Therefore, the use of stimulus/restimulus vectors as target variables should be avoided")

### DB 8 description
- 10 subjects able-bodied + 2 right-hand transradial amputees
- 3 datasets collected from each subject
  - Dataset 1 & 2: 10 repetition/movement
  - Dataset 3: 2 repetition/movement
- Each dataset consists of
  - 9 movements + rest
  - movements performed bilaterally
  - movement duration: 6-9 sec + 3 sec rest
  - Each trial includes reaching the position (flexion) then extension
- Can use datasets 1 & 2 for training and hyperparameter tuning, dataset 3 for testing, or merge 1 & 2 and do a 
  cross-validation then test on 3.

## Accelerometer, Gyroscope and Magnetometer sensors: what are they measuring?
*Extracted from [this blog](https://www.maximintegrated.com/en/design/technical-documents/app-notes/5/5830.html), 
and [this cool blog](https://learn.sparkfun.com/tutorials/gyroscope/all)*

- **Micorelectromechanical systems (MEMS)** are components combining mechanical and electrical elements into a small 
  devices (of size in the micrometer range).
- **Accelerometer sensor** measures the acceleration (obviously 😀) ($m/s^2$). Recap high-school physics, 
  according to Newton's Second law of motion: the $acc \propto force$. It measures either static or dynamic 
  acceleration. In static acceleration, there is a constant force acting on 
  the object (eg. gravity, friction). Dynamic acceleration, the acting forces are non-uniform, for example, car 
  crashing leading to acceleration. ![](/blog/figures/acceleration_translation_rotation.png)
- **Gyroscopes** measure deflection from a given orientation and angular velocity. Said differently, they measure 
  rotational motion (in $\circ/s$ or revolutions per second). ![](/blog/figures/Gyroscope-components-and-gyroscopic-precession.jpg)
- **Magnetometer sensor** measures relative changes in magnetic field at a particular location.

---
## Muscle Synergies in sEMG
- In voluntary movement, the central nervous system (CNS) has its own way to coordinate muscle activations. We do not 
still 
know for sure how this is happening but one thing that we do know is that the CNS must be doing some sort of 
dimensionality reduction. This is referring to the fact that muscle activities are coordinated, synchronized. So the 
hypothesis is the CNS might be 
"representing all useful muscle patterns as combinations of a small number of generators"  [d'Avella, A., Saltiel, P. 
& Bizzi, Nat Neurosci, 2003. ](d'Avella, A., Saltiel, P. & Bizzi) in order to   
allow for a wide range of degrees of freedom and great flexibility. In other words, **there is only a small subset of 
controllers (i.e muscle synergies) that are combined in space and time to generate many muscle activity 
patterns.**

- People usually analyze such coherent activations 
of muscles using muscle synergies analysis. This refers to analyzing muscle patterns to extract the underlying 
"sources" for the observed muscle patterns. The generated muscle patterns are models are a "combinations of 
time-varying muscle synergies, that is, coordinated activations of a group of muscles with a specific time course 
  for each muscle" [d'Avella, A., Saltiel, P. 
& Bizzi, Nat Neurosci, 2003. ](d'Avella, A., Saltiel, P. & Bizzi). 

**Note**: It seems a very similar idea to **blind source separation** for decomposing the sources from a mixed 
signal (more on that later 🙃)