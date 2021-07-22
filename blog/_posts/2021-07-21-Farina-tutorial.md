---
layout: post
title: Vecchio et al. (2020) - Tutorial, Analysis of Motor Unit Discharge Characteristics from High-Density Surface EMG Signals
tags: [Motor units]
include_toc: true
---
The paper can be found [here](https://www.sciencedirect.com/science/article/pii/S1050641120300419?via=ihub).

**Disclaimer:** For this tutorial paper, I will follow a different structure for the post; it would resemble more a college student lecture notes 🤓.

---
## Why am I reading this tutorial paper?
To better understand whether we really care about the precise timings of the motor unit discharges or only their spiking frequency that matters for muscle control. This question goes back to the famous debate of rate vs. time-based computation.

After going through the paper, I noticed that the question is not addressed but still I found it an interesting paper. It goes into details of the EMG data acquisition, decomposition and visual inspection of the results of the decomposition. I might update this post later when I read these sections in more details.

---
## Extracting neural information from HD-EMG
![MUAPs_EMG](/blog/figures/farina_tutorial_MUAP_EMG.png)
  
- EMG signal is affected by the timing of the discharges and the waveform of the APs of the MUs since it is the algebraic summation of these motor units APs.

1. **What factors affect the characteristics of MUAPs (MUAP amplitude)?** 
   
   First of why this question is important 😀? since MUAPs directly relates to the EMG we might want to know how the shape of the MUAPs comes about (because this would relate to the observed EMG signals).
   - Conduction velocity which is proportional to (scales with) the muscle fiber
   - Number of innervated muscle fibers which is related to the MU recruitment threshold. However, the association of MUAP amplitude and MU recruitment threshold is not very straightforward.
          
2. **What are the problems with relying on the EMG amplitude to estimate the neural drive?**
   
 > **Note:** For a more detailed description of the limitations of the spectral and amplitude features of  EMG to infer neural strategies of muscle control, I refer you to the paper by Del Vecchio et al., *Associations between motor unit action potential parameters and surface EMG features*, (2017).

   - From what I just described above, the association between recruitment threshold and MUAP amplitude is weak as it depends on the distance between muscle fibers and recording electrodes. This means that the association between EMG amplitude and strength of neural drive is not very "clean". As such the link between EMG amplitude and force.
   - EMG amplitude varies across subjects, muscles and time; which makes comparisons across tasks, individuals challenging.
   - Simulation results of EMG generation revealed that the amplitude feature of the signal is only a crude indicator of neural drive. 
        - How did they reach this conclusion? they tested the link between MUAPs (which gives rise to EMG) and recruitment thresholds and found these two variables to be unrelated.
   - On the other hand, the estimated conduction velocity of the MUAPs was showed to be associated with the MU recruitment threshold across subjects and muscles. It forms therefore a more stable basis for estimating the neural drive. I guess what the authors are trying to convey here is that extracting features from the motor unit themselves is a better way to predict the neural drive compared to global features of sEMG.

These challenges (to interpret features form sEMG) has pushed the research community to start looking onto iEMG and decomposition techniques. These approaches give a direct estimate of the neural drive through the identification of the MU discharge times.

---
## What can we know from the motor units discharge/ properties?
- **Recruitment threshold**: it directly maps to force when the first motor unit AP occurs. Here the force is the once produces by the muscle fibers innervated by the motorneuron. This force occurs with a delay that depends on the conduction velocity of the axons and the properties of the muscle fibers (active/passive)
    - How to estimate the recruitment threshold of the MUs?
         - Given this delay characteristic, we would have to measure the discharge properties of the MUs as the subject follows a trapezoidal force trajectories with controlled rates of increase/decrease in force (typically 5-20% MVC/s till they reach a plateau at 35-70% of maximal force).
        - Measuring the recruitment/de-recruitment thresholds can be obtained by looking at the raster plots of the identified motor units. We can clearly see at which force level a new motor unit is being activated.
          
![MU_recruitment_threshold](/blog/figures/farina_tutorial_recruitment_threshold.png)

- **Common synaptic input**: we can extract the characteristics (in time and frequency domains) of the common input to the motorneuron pool.
    - Time domain: using cross-correlogram (cross-correlation) between the motor unit discharges.
    - Frequency domain: we can estimate the frequency bands of this common input using coherence function which can be thought of a cross-correlation analysis in the frequency domain.
    
- **Strength of persistent inward currents (PICs)**: these are the currents coming into the motorneurons and can reflect neuromodulatory inputs received by motorneurons.
  
- **Other physiological information**: such as the motor unit size can be extracted from the amplitude and conduction velocity.


In that sense, the MU discharge times and characteristics give us access to a more accurate view of the neural drive and physiological properties which can be exploited to design intuitive controllers.