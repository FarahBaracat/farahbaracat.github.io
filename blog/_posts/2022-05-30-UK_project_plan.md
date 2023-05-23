---
layout: post
title: Project in Dario Farina's Lab - General Plan
tags: [ICL Project]
include_toc: true
---

## Questions I need to research
- How is proportional control generated from the upper stream pathway all the way down to lower motor neurons?
- How do lower motor neurons activity lead to proportional muscle activation? do they have an instantaneous 
  firing rate that can be mapped directly (e.g. using linear 
  regression) to movement kinematics (i.e force, speed, position)?
- What is new about online ICA? how does it compare to attempts of online Convolution Kernel Compensation 
  (CKC) method 
  for 
  motor 
  neurons 
  decomposition?
- What is the advantage of combining motor neurons with a spiking net? Yes, we talk a lot about a neural interface 
  that "speaks the same language" as biological neurons but do we really need that? What is the main advantage apart 
  from power consumption? If it is true that motor neurons firing rates can directly (i.e linear) map to motion, 
  then we don't really care at all about exact spike times, right?
- Refresh on isometric vs. isotonic contractions + variables they control (force) + motor neurons control properties.


---
## Interesting points to investigate
- Can we achieve simultaneous proportional control (SPC) from MU using a spike-based approach? or do we not need the 
  pattern of discharge timings at all and can only rely on rate-based network?
- For SPC, what are the challenges in mapping firing rates to kinematics variables? It doesn't look like an easy 
  problem, but I have no clue why 😀
- In the case of classification relying on motor neurons, as noted also in the paper of Simone Tanzerlla (2021), the 
  number of identified motor neurons varies between subjects. This is due to the variability in the identified motor 
  unit action potentials. These waveforms depend on the volume conduction which varies across subject and across 
  session (it is related to electrode displacement and even more anatomical aspects such as muscle shape, body 
  metric, ...).  With variable motor neurons, the network input layer varies between subjects. 
  - One approach would be to train a network per subject and session but that is non-optimal.
  - Another approach could be to have an input layer with N inputs  (N motor neurons commonly identifies across the 
    recording sessions) and retrain addition n input (connections) for each session separately.
  - As for the output layer, we can use continual learning to increase the number of learnt tasks

- How can we learn the decomposition using Deep Learning approach or even better spike-based approach?
---

## Previous work on motor neurons for control
**[(2021) Proportional and simultaneous control using motor neurons](https://iopscience.iop.org/article/10.1088/1741-2552/abf186)**
- This work uses the decomposed motor unit spike trains from sEMG to control wrist and hand movement *online* (<mark>3 
  DoFs only</mark>: wrist flexion/extension/grasp in Exp1 or pronation/supination/grasp in Exp2). The *simultaneous* 
  control part is when the subjects had to control <mark>2 DoFs concurrently </mark>(either flexion/extension + grip or 
  pronation/supination + grip) 

- They propose 2 phases to carry out the decomposition:
    - **Calibration phase**: this is completed offline and is used to extract the decomposition parameters 
      (cross-correlation vector, $c_{t_j,\bar y}$)
    - **Online phase**: using the obtained decomposition parameters, get spike trains of the jth MU using equation 1.
      This is simply achieved by using windows of the preprocessed EMG signal. There is also sth about using 
      Kmeans++ to get the cluster centroids (which I honestly didn't quite get yet 😅)
  <p align="center"><img src="/blog/figures/CKC_MU_eq.png" alt="drawing" width="420"/></p>

- 3 pipelines were compared, as shown below. The aim is to contrast the performance of conventional control methods 
  to the MU-based.
  <p align="center"><img src="/blog/figures/pipeline_comparison_chenchen_2021.png" alt="drawing" width="700"/></p>
    - For the MU-based controller, they relied on a simple linear regressor on the instantaneous discharge rate of the 
  cumulative spike 
  train (calculated by combining all MU spike trains in each MU pool) to map to motion activation level. In other 
  words, they were not inferring movement kinematics. **They mapped the firing rates to a continuous scale for each 
  motion (i.e DoF) separately**. Also note that this is validated in a virtual 
  environment and 
  not on real tasks.
> The projection from MU discharges to kinematics is a complex issue with multiple variables. In this work, the MU activities were mapped to the activation level of each motion, rather than any specific kinematic metrics. Additionally, this simple mapping method was proved to be efficient for proportional control.


**[(2019) Finger angle estimation from EMG using ICA and linear regression](https://www.frontiersin.org/articles/10.3389/fnbot.2019.00075/full)**
- An interesting argument why we need an input feature for the controller that is not EMG: for fine manipulation, 
  where we need to control fingers, the muscles we are recording from are small and hence the placement of the 
  electrodes would highly affect the recorded signals and therefore "significantly affect the accuracy and precision 
  of the joint angles and forces".
- The aim is to control fingers **separately**.



**[(2021) Neuromorphic decoding of hand gestures from spinal motor neurons](https://assets.researchsquare.
com/files/rs-1465054/v1_covered.pdf?c=1647636892)**
- The aim is to decode 10 hand movements using decomposed motor neurons using CKC. The network used is a 
  convolutional 
  SNN.
- The dataset used in this work is big: recording from 14 intrinsic and extrinsic muscles, 5 healthy subjects, 10 
  natural gestures.
- They also track motor neurons (MN) across tasks for each subject by concatenating the EMG recording from all the 
  tasks 
  performed by each subject.
- The identified motor neurons are used as input to a SNN. Since the number of MN varies per subject, they train 5 
  different SNN (one per subject). This is the *intra-subject* approach. Another tested approach is to identify a 
  common set of motor neurons across tasks and subjects and use that as input to a single network (*inter-subject* 
  approach).
- SNN topology consists of 2 convolutional layers. Each layer is trained separately on 10 classes (not very obvious 
  why this choice) with surrogate gradient.
<p align="center"><img src="/blog/figures/DECOLLE_Simone.png" alt="drawing" width="700"/></p>
---
## Some quick notes on ICA
- The idea behind is to identify the Independent Component (IC) in a mixture. So we can denote x as the observation 
  signal:

  $x = A. s$;

where A is a "full-rank" matrix containing the mixing information (can't really recall what that was, will look it up 
later :D)  and s are the independent sources.

- Now we need to estimate s and make sure that the identified sources are (guess what :D) independent 🥳. In order to 
  guarantee that, we somehow need an objective function or a metric to quantify that. Those measures are mutual 
  information and negentropy. The independence of the sources is hence measures by contrast, hence why we talk about 
  **contrast functions** (getting the 
  difference)
  od each variable distribution and the Gaussian.


## Some notes on Ridge Regression
- A technique to analyse "multiple regression data that suffer from multicollinearity"[here](https://ncss-wpengine.netdna-ssl.com/wp-content/themes/ncss/pdf/Procedures/NCSS/Ridge_Regression.pdf)

So what is **multicollinearity**? 
- when there is a near-linear relationship among the independent variables.
- It can create bias in the estimates of the regression coefficients.


## Notes on temporal convolution network
**To Read: [nice paper,2018](https://arxiv.org/abs/1803.01271)**




### Terminology and definitions
- [Extrinsic vs. Intrinsic muscle groups](https://www.joionline.net/library/show/muscles-of-the-hand-2/)
  - Extrinsic muscle groups are "are the long flexors and extensors. They are called extrinsic because the muscle belly is located on the forearm." 
  - Intrinsic group "is the smaller muscles located within the hand itself. The hand muscles are innervated by the 
    radial, median, and ulnar nerves from the brachial plexus"

---
## What is the input to motor neurons and how do they modulate muscle force exertion?
- Spikes from a single motor neuron is the result of an integration operation at the spinal level between the 
  central supraspinal commands and the peripheral afferent commands performed by modules of interneurons.
- Motor neurons are then recruited following the size principle. The number of recruited motor neurons and their 
  firing rate determine the overall control signal sent to modulate the muscle force exertion.
- "Two terms to describe the anatomical relationship between motor neurons and muscles" [for more details](https://nba.uth.tmc.edu/neuroscience/m/s3/chapter01.html):
  - Motor neurons are clustered into pools (i.e **<mark>motor neuron pools</mark>**). All motor neurons in one pool 
    innervate a 
    single muscle. There is a <mark>1-to-1 relationship between a muscle and a motor neuron pool</mark>.
  - Individual muscle fibers in a muscles are innervated by a single motor neuron. 
  - A single motor neuron can innervate more than one muscle fiber.
  - A **<mark>motor unit</mark>** is the combination of an individual motor neuron and all the muscle fibers it 
    innervates.
  - An **innervation ratio** refers to the number of fibers innervated by a motor neuron.
