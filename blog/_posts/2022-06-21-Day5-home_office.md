---
layout: post
title: Day 5 in Farina's Lab - Muscle contractions and transradial prostheses
tags: [ICL Project]
include_toc: true
---
## List of topics I would like to know about
- Previous work in the literature focused on simultaneous wrist movements?
- PID controllers
- Synergies in MUs 
- Relation between speed of movement and MU activity

## Terminology
- Tension is a _pulling_ force. Muscle tension is then the amount of contraction force in the muscle that is leading 
  to pulling on the tendons.
  - Muscle forces are measured with load cells. Load cells are force transducers; they convert an input mechanical 
    load, weight, tension, compression or pressure into an electrical output signal. This is the type of signal they 
    show when they say we give a real-time feedback or visualize force profile.
- When muscles contract, we talk about the force of those contractions
- There are different types of motor units (= motor neuron + muscle fibers they innervate):
  - Small motor neurons innervate few fibers and generate small forces (typically those neurons innervate small "red" 
    muscle fibers that contract slowly and generate small forces). "Red" because they are rich in capillary beds; 
    they are hence more resistant to fatigue. These are **slow MUs**, important for sustained muscular contraction 
    (help us maintain upright posture). These slow MUs have a low threshold of activation, meaning that they require 
    only a small synaptic input.
  - Larger motor neurons innervate large, pale muscle fibers that generate more force but have sparce mitochondria 
    and hence are easily fatigued.  These are **fast fatigued MUs**, important for generation of brief large forces.
  - **Fast fatigue-resistant MUs** lie somewhere in between the 2 classes. They are of intermediate size and are not 
    as fast as type 2.
  

##  Review Trans-radial Prostheses
### what are the currently available prostheses and DoFs
- Recap that trans-radial is below elbow amputation.
- There are broadly 3 types of trans-radial prostheses: cosmetic, body-powered and externally powered
- Human hand and wrist has 27 DoFs.
- The main grips used in daily living: power grip, lateral grip and precision grip