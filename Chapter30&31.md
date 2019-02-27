---
title: "Chapter 30: Compression Bound & Chapter 31: PAC-Bayes"
---
# Compression Bounds

Basic concept:
If a learning algorithm can express the output hypothesis using small subset of training set, then the hypothesis on the rest of the examples estimates its true error.

Shortly speaking, an algorithm that can "compress" its output is a good learner.

### Learning protocol to motivate the result:

#### Notation and assumption:
* Sample a sequence of $\mathit{k}$ examples, denoted $\mathit{T}$
* Construct a hypothesis $\mathit{h}_{T}$ based on $\mathit{T}$
* Sample a fresh sequence of $m-k$ examples $V$, calculate the error of $\mathit{h}_{T}$ on $V$

Since $V$ and $T$ are independent, by using Bernstein's inequality, we get 

LEMMA 30.1,
Assume that the range of the loss function is [0,1]. Then, \[\mathbb{P}\lbrack L_{D}(h_{T}) - L_{V}(h_{T}) \geq \sqrt{\frac{2L_{V}(h_{T})\log (1/\delta)}{\lvert V \rvert }} + \frac{4\log (1/\delta)}{\lvert V \rvert}  \rbrack \leq \delta\]


