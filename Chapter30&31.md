---
title: "Chapter 30: Compression Bound & Chapter 31: PAC-Bayes"
---
# Compression Bound
Basic concept:
If a learning algorithm can express the output hypothesis using small subset of training set, then the hypothesis on the rest of the examples estimates its true error.
Shortly speaking, an algorithm that can "compress" its output is a good learner.

###Learning protocol to motivate the result
Notation and assumption:
1.Sample a sequence of \mathit{k} examples, denoted \mathit{T}
2.Construct a hypothesis \mathit{h}_{T} based on \mathit{T}
