---
layout: post
title: Daily Logs - Starting a new sEMG Project using NinaProDB
tags: [sEMG Project]
include_toc: False
---
## Aim
To better understand the characteristics of sEMG signals and their relation to the recorded kinematics (eg. joint 
angles, fingers position, speed,...etc. ). For this, the plan is to use the publicly available datasets from [NinaPro 
Database](http://ninaweb.hevs.ch).

Eventually the ultimate goal is to research how to perform regression on the joint angles. Since the best way to 
learn is by doing, I will also code.

The main questions 
I am 
planing to answer are:
- What is the current state-of-the-art (SoA) for this task?
- What are the current limitations of these SoA? (e.g. deployment, memory, power consumption, precision, latency,...)

## Day 1: April 10, 2022 
### Today's Progress
- Setup this blog series
- Read about the dataset I will use and muscle synergies ([My notes](2022-04-10-ninapro_description.md))


### Thoughts
Extremely excited to start this project yet very tired already. Woke up at 3.30 am and its almost 8 am now...will 
probably go back to sleep now :D

----
## Day 2: April 12, 2022
- Not very productive, was skimming through for papers on regression-based control [notes](2022-04-12-zshell.md).

---
## Day 3: April 21, 2022
### Today's Progress
- Spend a good amount of time (maybe 2 hours) debugging how to build my website. I had problems after upgrading to 
a new bundler version (e.g website not building, live-reload not working, unable to do bundle update or install,... )
- Started EDA notebook (loading data, some initial visualization and statistics) 💪🏼 [(Git 
  Repo)](https://github.com/FarahBaracat/ninapro_db8)
- Some literature review on proportional control ([My Notes](2022-04-21-proportional_control.md))

### Thoughts
Great progress today, still a long way to go.


---
## Day 4: April 24, 2022
### Today's Progress
- Wrote the project description for [Capocaccia's workshop](https://capocaccia.cc/en/)
- Some minor additions to the EDA notebook: computing the stimuli correlations.

---
## Day 5: April 26, 2022
### Today's Progress
- In the past days, I was working on the demo for Capocaccia's 2022 with the MIA hand. We wanted to have a pipeline 
  ready in which a spiking neural network is mapped onto a neuromorphic chip which interfaces with the hand.
- Continued working on the [EDA notebook](https://github.com/FarahBaracat/ninapro_db8)