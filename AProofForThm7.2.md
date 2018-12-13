---
title: "Thm. 7.2"
---

## A Proof Proposal for Theorem 7.2

**Theorem 7.2:**
A hypothesis class $\mathcal{H}$ of binary classifiers is nonuniformly learnable if and only if it is a countable union of agnostic PAC learnable hypothesis classes.

**Proof Proposal:** 

"$\Leftarrow$" as in the book.

"$\Rightarrow$" 
Assume that $\mathcal{H}$ is nonuniform learnable using some algorithm $A$.
For every $n \in \mathbb{N}$ let 
$$ \mathcal{H}\_n := \\{ h \in \mathcal{H} : m\_{\mathcal{H}}^{NUL} (1/8, 1/7, h) \leq n \\} \\.$$
It follows that $\mathcal{H} = \bigcup\_{n \in \mathbb{N}} \mathcal{H}\_n$.

We prove the "$\Rightarrow$" claim by contradiction. 
I.e., assume that $\mathcal{H}\_n$ is not APAC learnable then we find a contradiction to its definition:

Suppose $\mathcal{H}\_n$ is not APAC learnable. 
Then, by the fundamental Theorem (Thm. 6.7) $\mathcal{H}\_n$ has infinite VC-dimension.
(Note, that this implies that the domain $\mathcal{X}, on which $\mathcal{H}$ operates must be infinite, as well).
$A$ is a learning algorithm for the class of binary classificators with $0-1$-loss.
Thus, the No-Free-Lunch Theorem (Thm. 5.1) applies for $\mathcal{H}\_n$ and all $n' \in \mathbb{N}$.
(In particular, it does not require $A$ to output anything more specific than a function $f: \mathcal{X} \to \{0,1\}$.)

That is:

$ \forall n' \in \mathbb{N} \exists $ a distribution $D$ that is realizable by $\mathcal{H}\_n$ s.t. with probability $ \geq 1/7$ over the choice of $ S ~ D^{n'}$ it holds that $L\_D (A(S)) \geq 1/8$. 

However, by definition of $\mathcal{H}\_n$ we have $\forall h\in \mathcal{H}\_n : m\_{\mathcal{H}}^{NUL} (1/8, 1/7, h) \leq n$.
That is, $ \forall D \forall h \in \mathcal{H}\_n : L_D (A(S)) \leq L_D(h) + 1/8 $ with probability $\geq 6/7$ over the choice of $S ~ D^n$.

Considering the case $n' = n$ yields the desired contradiction.
Hence, $\mathcal{H}\_n$ must be agnostic PAC learnable. 

