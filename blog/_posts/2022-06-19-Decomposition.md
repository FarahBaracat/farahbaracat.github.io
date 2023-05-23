---
layout: post
title: Weekend Readings
tags: [ICL Project]
include_toc: true
---

# Decomposition Algorithm
From [here](https://www.fon.hum.uva.nl/praat/manual/blind_source_separation.html)
Blind source separation (BSS) are common techniques used to "blindly" extract sources from a mixture (observed) at 
multiple sensors (or channels). 
There are 
two 
types of mixtures: instantaneous mixture and a convolutive mixture:
- Instantaneous mixture: doesn't take into consideration reverberation in a room for instance when dealing with audio 
  signals. It is "instantaneous"; modeled by Y the observed signal. 
$Y = A. X$ where A is the mixing matrix, X are the independent sources signals.

This means that the observed signal is nothing but a linear combination of the same sources (note that there is no 
time component here)

- Convolutive mixture is modeled by an h filter characterizing the propagation of the signal in the medium. For MU 
  decomposition, this h filter is the MUAP 
$y_i(n) = \sum \sum h(\tau) x(n-\tau) + N(n)$

Convolutive mixture are harder to solve which is why in the case of CKC or ICA, they transform the problem into an 
instantaneous mixture by adding delayed replicas to the observation and sources matrices [more on this later]. This 
is just a way of re-writting the convolution operation into a simple matrix multiplication
> Solutions for convolutive mixture problems are much harder to achieve. One normally starts by transforming the problem to the frequency domain where the convolution is turned into a multiplication. The problem then translates into a separate instantaneous mixing problem for each frequency in the frequency domain. It is here that the indeterminacy problem hits us because it is not clear beforehand how to combine the independent components of each frequency bin.




