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

Since $V$ and $T$ are independent, by using Bernstein's inequality, we get the following lemma

**Lemma:**

Assume that the range of the loss function is [0,1]. Then, 

$\mathbb{P}\lbrack L_{D}(h_{T}) - L_{V}(h_{T}) \geq \sqrt{\frac{2L_{V}(h_{T})\log (1/\delta)}{\lvert V \rvert }} + \frac{4\log (1/\delta)}{\lvert V \rvert}  \rbrack \leq \delta$

Then, we redefine the protocol as follow,
* Agree on a sequence of k indices $I = (i_{1},...,i_{k})\in [m]^{k}$
* Sample a sequence of $m$ examples $S = (z_{1},...,z_{m})$
* Define $T = S_{I} = (z_{i_{1}},...,z_{i_{k}})$ and $V$ be the rest of the examples in $S$

This protocol is still equivalent to the protocol we defined before, the previous lemma still holds.

Applying a union bouond over the choice of the sequence of indices to obtain the following theorem,

**Theorem:**

Let $k$ be an integer and let $B$ : $Z^{k} \to \mathcal{H}$ be a mapping from sequence of $k$ examples to the hypothesis class. Let $m \geq 2k$ be a training set size and let $A: Z^{m} \to \mathcal{H}$ be a learning rule that receives a training sequence $S$ of size $m$ and returns a hypothesis such that $A(S) = B(z_{i_{1}},...,z_{i_{k}})$ for some $(i_{1},...,i_{k})\in [m]^{k}$. Let $V = {z_{j}:j \not\in (i_{1},...,i_{k})}$ be the set of examples which were not selected for defining $A(S)$. Then, with probability of at least $1 - \delta$ over the choice of $S$ we have

$L_{D}(A(S)) \leq L_{V}(A(S)) + \sqrt{L_{V}(A(S))\frac{4k\log (m/\delta)}{m}} + \frac{8k\log (m/\delta)}{m}$

Then a direct corollary could be obtained:

**Corollary:**

Assuming the condition of Theorem 30.2, further assuming that $L_{V}(A(S)) = 0$, then, with probabilit of at least $1-\delta$ over the choice of S we have

$L_{D}(A(S)) \leq \frac{8k\log (m/\delta)}{m}$

These results lead to the final definition of Compression Scheme,

**Definition of Compression Scheme:**

Let $\mathcal{H}$ be a hypothesis class of functions from $\mathcal{X}$ to $\mathcal{Y}$ and let $k$ be an integer. We say that $\mathcal{H}$ has a compression scheme of size $k$ if the following holds:
For all $m$ there exists $A : Z^{m} \to [m]^{k}$ and $B : Z^{k} \to \mathcal{H}$ such that for all $h \in \mathcal{H}$, if we feed any training set of the form $(x_{1},h(x_{1})),...,(x_{m},h(x_{m})$ into $A$ and then feed $(x_{i_{1}},h(x_{i_{1}})),...,(x_{i_{k}},h(x_{i_{k}})$ into $B$, where $(i_{1},...,i_{k})$ is the output of $A$, then the output of $B$, denoted $h^\prime$, satisfies $L_{S}(h^\prime) = 0$.

For unrealisable sequences,

Let $\mathcal{H}$ be a hypothesis class of functions from $\mathcal{X}$ to $\mathcal{Y}$ and let $k$ be an integer. We say that $\mathcal{H}$ has a compression scheme of size $k$ if the following holds:
For all $m$ there exists $A : Z^{m} \to [m]^{k}$ and $B : Z^{k} \to \mathcal{H}$ such that for all $h \in \mathcal{H}$, if we feed any training set of the form $(x_{1},y_{1})),...,(x_{m},y_{m})$ into $A$ and then feed $(x_{i_{1}},y_{i_{1}}),...,(x_{i_{k}},y_{i_{k}})$ into $B$, where $(i_{1},...,i_{k})$ is the output of $A$, then the output of $B$, denoted $h^\prime$, satisfies $L_{S}(h^\prime) \leq L_{S}(h)$.



