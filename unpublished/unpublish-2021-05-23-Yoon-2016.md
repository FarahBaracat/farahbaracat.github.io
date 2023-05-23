<!-- [comment]: <> (---)

[comment]: <> (layout: post )

[comment]: <> (title: Yoon &#40;2016&#41; -  LIF and Simplified SRM Neurons Encode Signals Into Spikes via a Form of Asynchronous)

[comment]: <> (        Pulse Sigma–Delta Modulation )

[comment]: <> (tags: [Neuron models approximated with a form of ADM])

[comment]: <> (include_toc: true)

[comment]: <> (---)


[comment]: <> (Link to the paper [here]&#40;https://ieeexplore.ieee.org/document/7419261&#41;.)



[comment]: <> (## Why am I reading this paper?)

[comment]: <> (As I am trying to characterize &#40;and quantify&#41; the effect of the **asynchronous delta modulator &#40;ADM&#41;** parameters on the information content and frequencies of the input signal, one suggested idea was to tap into what "we" &#40;the neuroscience community 🙃&#41;  already know about how biological neurons encode a continuous-time signal.)

[comment]: <> (By relying on the similarity between an ADM and a neuron's encoding mechanism, we can extend our knowledge about the effect of neural encoding on the frequency and information content of any input signal to derive an analytical expression for the ADM.)

[comment]: <> (Therefore, a first stop is to understand how to relate the ADM and neuron encoding. I initially came across this paper in [Zambrano & Bohte &#40;2016&#41;]&#40;{% post_url 2021-05-23-Bohte-2016 %}&#41;.)

[comment]: <> (----)

[comment]: <> (## Motivation)

[comment]: <> (Tha main motivation of this line of research is to understand how various neuron models encode continuous-time signals into spikes.)


[comment]: <> (**Disclaimer**)

[comment]: <> (This is not the very first work trying to decipher the mechanisms of neural encoding/decoding. Previous work have investigated how spiking neurons models &#40;e.g. **integrate-and-fire &#40;IF&#41;** neuron, **leaky integrate-and-fire &#40;LIF&#41;**, **spike response model &#40;SRM&#41;**&#41; encode/decode signals into spikes.)

[comment]: <> (This work can thus be seen as complementary to these studies relating neuron models to a special form of **sigma-delta modulation &#40;SDM&#41;** which is the primary paper's contribution.)

[comment]: <> (**Why does it matter?**)

[comment]: <> (An understanding for biological neural encoding/decoding can:)

[comment]: <> (1. Help us understand how to design efficient low-power encoder and artificial neural networks.)

[comment]: <> (2. Guide how we design decoders that can reconstruct the encoded signals from spikes.)

[comment]: <> (3. Pave the way to designing algorithms that can make sense of the generated spikes for further processing.)

[comment]: <> (---)

[comment]: <> (## Main  Contribution)

[comment]: <> (Shows a direct correspondence between 2 types of spiking neuron models, LIF and the simplified SRM, and a  form of asynchronous sigma-delta modulation, referred to as **Asynchronous-Pulse-Sigma-Delta Modulation &#40;APSDM&#41;**.)

[comment]: <> (This work is restricted to the encoding mechanism of a single neuron as opposed to population coding.)

[comment]: <> (**How are the SDM and APSDM different?**)

[comment]: <> (- SDM is clock-based, uniform time sampling. The input signal is encoded into a sequence of bits &#40;binary&#41;)

[comment]: <> (- Asynchronous Pulse SDM has no clock; it is event-based sampling. The signal is encoded into a train of time-encoded impulse functions. )

[comment]: <> (---)

[comment]: <> (## Methods)

[comment]: <> (The paper is structured into 4 parts. For the sake of this summary, I will focus on the first part of relating the SRM neuron to the APSDM framework.)

[comment]: <> (1. **Part one** uncovers how LIF and SRM neuron equations can be re-written to match their defined APSDM framework.)

[comment]: <> (2. **Part two** provides a detailed description of the APSDM encoder &#40;a circuit's perspective&#41;.)

[comment]: <> (3. **Part three** uncovers the design of a linear, closed-form decoding filter to reconstruct the continuous-signal from spikes.)

[comment]: <> (4. **Part four** compares APSDM to a SDM with supporting examples.)

[comment]: <> (---)

[comment]: <> (## Details: Relating the $SRM_0$ to APSDM)

[comment]: <> (#### A. Interlude on Simplified SRM neuron &#40;$SRM_0$&#41;)

[comment]: <> (-  The membrane voltage, $V_{SRM_0}$ is defined as a filter response. The model can be easily framed then as a signal processing module.)
   
[comment]: <> (![SRM_eq]&#40;/blog/figures/SRM_equation.png&#41;)

[comment]: <> (- $v_{SRM}&#40;t&#41;$ is the summation of 3 terms:)

[comment]: <> (1. Input current response: $i&#40;t&#41; * \kappa_0&#40;t&#41;$; where $\kappa_0&#40;t&#41;$ is the input current response filter.)

[comment]: <> (2. Reset response: $\sum_{m=1}^{M_{SRM}} \eta &#40;t - T_m^{SRM}&#41;$ denoting the reset response train.  $\eta&#40;t&#41;$ represents the response of the neuron to its own generated spikes indexed by $m$ &#40;$M_{SRM}$ is the total number of output spikes&#41;)

[comment]: <> (3. Voltage contributions from presynaptic neurons: $v_{SRM}^{PSP}&#40;t&#41;$)

[comment]: <> (**But what is the reset response? How is it related to the spike generation mechanism?**)

[comment]: <> (- At the time $t = t_0$ when the threshold voltage is exceeded, $V_{SRM}&#40;t&#41; > v_{t}$ , the reset response is activated. In other words, a negative-valued, decaying function $\eta&#40;t-t_0&#41;$ is added to $V_{SRM}&#40;t&#41;$ to drive it back toward the reset voltage $v_r$.)

[comment]: <> (- Given this view, we can now see that the second term is a train of reset responses generated as a result of a train of output spikes, $s_{SRM}&#40;t&#41;$:)

[comment]: <> (  $s_{SRM}&#40;t&#41; = \sum_{m=1}^{M_{SRM}} \delta&#40;t - T_m^{SRM}&#41;$)

[comment]: <> (#### B. Signal encoding with $SRM_0$)

[comment]: <> ($V_{SRM_0}$ can be expressed in a different form highlighting the effect of the reset response:)

[comment]: <> ($V_{SRM}&#40;t&#41; = y_{SRM}&#40;t&#41; - \hat y_{SRM,L}&#40;t&#41;$)

[comment]: <> (- The first term now describes an "unconstrained membrane potential", $y_{SRM}&#40;t&#41;$, while the second is the positive version of the reset response train, $\hat y_{SRM,L}&#40;t&#41;$.)

[comment]: <> (- The signal encoding can thus be seen as in the figure below:)

[comment]: <> (![SRM]&#40;/blog/figures/SRM0neuron.png&#41;)


[comment]: <> (#### C. APSDM)

[comment]: <> (In the paper, the author presents two forms of the APSDM, for the sake of this summary, I only describe the encoder of Form 1. Note that an APSDM consists of an encoder, a channel and a decoder.)

[comment]: <> (##### APSDM Encoder Block)

[comment]: <> (- Consists of a sigma filter, $g_\Sigma&#40;t&#41;$ , which shapes the input $i&#40;t&#41;$ &#40;$y&#40;t&#41;$&#41; before it is fed into an APDM encoder.)

[comment]: <> (- APDM encoder subtracts a smoothed reconstructed version of $y&#40;t&#41;$ denoted $\hat y &#40;t&#41;$.)

[comment]: <> (- The difference, $v&#40;t&#41;$ is input to a quantizer with a single threshold at $\Delta /2 $ forming $\hat v&#40;t&#41;$.)

[comment]: <> (- At each time $\hat v&#40;t&#41; = 1$ an impulse is generated by the pulse generator block.)

[comment]: <> (- The output train of impulses $s&#40;t&#41;$ is fed to a delta filter $g_\Delta &#40;t&#41;$ which output a locally reconstructed version, $\hat y &#40;t&#41;$.)

[comment]: <> (![APSDM]&#40;/blog/figures/APSDM.png&#41;)

[comment]: <> (#### D. Similarity)

[comment]: <> (From the block diagrams, we can easily see the one-to-one correspondence between the two systems. )

[comment]: <> (Both consists of 2 processing blocks: )

[comment]: <> (- **A feedforward filter**: sigma filter for the APSDM and input current response  $\kappa_0&#40;t&#41;$ for the $SRM_0$ neuron.)

[comment]: <> (- **A spike generation and feedback block**:  takes the filter output and generates a train of impulses which is fed back through a positive reset response filter $-\eta &#40;t&#41;$ &#40;in the case of the $SRM_0$ neuron&#41; or a delta filter $g_\Delta &#40;t&#41;$ &#40;for the APSDM&#41;.) -->
