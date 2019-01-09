---
title: "Nonuniform Learnability & SRM"
---

# Nonuniform Learnability and Structural Risk Minimisation (SRM)

Remark: Let in the following $\mathcal{H}$ be a hypothesis space on a domain $X$, where $X$ is given an arbitrary probability distribution $\mathcal{D}$.

Uniform convergence is a very useful but not always available property of a hypothesis space. Luckily there is a weaker notion that still yields some information. We will later see how. First we recall two definitions.

Definition: We call $S\subset X$ $\epsilon$-representative for $\mathcal{H}$ if for all $h\in\mathcal{H}$
$$| L_{\mathcal{D}}(h)-L_S(h)| \leq \epsilon \text{.}$$

Definition: $\mathcal{H}$ has the uniform convergence property if there exists a function $m_{\mathcal{H}}^{UC}: (0,1)^2 \rightarrow \mathbb{N}$ such that for all $\epsilon,\delta>0$ and an i.i.d. drawn sample set $S\subset X$ with $\|S\|>m_{\mathcal{H}}^{UC}(\epsilon,\delta)$ we have with probability at least $1-\delta$ that 
$$ \forall h\in\mathcal{H} \quad |L_{\mathcal{D}}(h)-L_S(h)|<\epsilon \text{.}$$

In the case of uniform convergence we ask for a sample complexity that guarantees us with propability at least $1-\delta$ that a sample set of given size provides us for \emph{all} $h\in\mathcal{H}$ an empirical error that is in some sense representative for the true error. However this is often not possible. But instead we can compare hypotheses among each other. We already weakened the notion of PAC-learnability to agnostic PAC-learnability. That is, instead of the real classification we compared hypotheses to the best possible among them. We can weaken this even further by comparing hypotheses with any fixed element $\tilde{h}\in\mathcal{H}$.

Definition: Let $\tilde{h}\in\mathcal{H}$. We say that a hypothesis $h\in\mathcal{H}$ is $(\epsilon, \delta)$-competitive with $\tilde{h}$ if with probability at least $1-\delta$
$$L_{\mathcal{D}}(h)\leq L_{\mathcal{D}}(\tilde{h})+\epsilon \text{.}$$

Definition: $\mathcal{H}$ is called nonuniformely learnable if there exists an algorithm $A: \mathcal{P}(X) \rightarrow \mathcal{H}$ and a function $m_{\mathcal{H}}^{NUL}: (0,1)^2\times \mathcal{H} \rightarrow \mathbb{N}$ such that for all $\epsilon,\delta>0$, $\tilde{h}\in\mathcal{H}$ and an i.i.d. drawn sample set $S\subset X$ with $\|S\|>m_{\mathcal{H}}^{NUL}(\epsilon,\delta, \tilde{h})$ we have with probability at least $1-\delta$ that 
$$ L_{\mathcal{D}}(A(S)) \leq L_{\mathcal{D}}(\tilde{h})+\epsilon \text{.}$$

## Structural Rist Minimisation (SRM)

Assume that our hypothesis space has infinite VC-dimension. Even though we lose uniform convergence, there might still be certain structures we can exploit. Often we prefer some hypotheses over others. Reasons might be intuition, costs or implementation concerns. In those cases we can divide our hypothesis space into (not necessarily disjoint) subspaces and assign weights to them. If each of those subspaces has the uniform convergence property, we will infer nonuniform learnability.

Let $\mathcal{H}=\bigcup_{n\in\mathbb{N}} \mathcal{H}_n$ where each $\mathcal{H}_n$ has the uniform convergence property. We define 

$\nu: \mathcal{H}\rightarrow \mathbb{N}$, $h \mapsto \min\{ n\in\mathbb{N}: h\in\mathcal{H}_n\}$,

$\epsilon_n: \mathbb{N}\times(0,1) \rightarrow (0,1)$, $(m,\delta)\mapsto \min\{\epsilon\in(0,1): m_{\mathcal{H}_n}^{UC}(\epsilon, \delta)\leq m\}$.

Hence for all $m\in\mathbb{N}$, $\delta\in(0,1)$ we have with probability at least $1-\delta$ that 
$$ \forall n\in\mathbb{N}, \forall h\in\mathcal{H}_n \quad |L_{\mathcal{D}}(h)-L_S(h)|\leq \epsilon_n(m,\delta) \text{.}$$

Since $\mathcal{H}$ has infinite VC-dimension, we can't fix an $\epsilon>0$ and determine a sufficient sample size to achieve this bound (with probability at least $1-\delta$). Instead we first fix the sample complexity and regard the resulting bound on each $\mathcal{H}_n$, $n\in\mathbb{N}$. We now introduce weights on those subspaces. The following theorem shows why this is useful.

Definition: A weight function on $$\mathcal{H}=\bigcup_{n\in\mathbb{N}} \mathcal{H}_n$$ is a function $$\omega: \mathbb{N}\rightarrow [0,1]$$ such that $$\sum_{n \in\mathbb{N}} \omega(n)\leq 1$$.

Theorem: With probability at least $1-\delta$ we have that
$$ \forall n\in\mathbb{N}, \forall h\in\mathcal{H}_n \quad |L_{\mathcal{D}}(h)-L_S(h)|\leq \epsilon_n(m, \omega(n)\cdot\delta) \text{.}$$

Proof: $$P\left(\exists n\in\mathbb{N}, \exists h\in\mathcal{H}_n \quad \|L_{\mathcal{D}}(h)-L_S(h)\| > \epsilon_n(m, \omega(n)\cdot\delta)\right)$$ 

$$\leq \sum_{n\in\mathbb{N}} P\left(\exists h\in\mathcal{H}_n \quad |L_{\mathcal{D}}(h)-L_S(h)| > \epsilon_n(m, \omega(n)\cdot\delta)\right)
\leq \sum_{n\in\mathbb{N}} \omega(n)\cdot\delta \leq \delta$$.

Corollary: With probability at least $1-\delta$ we have that
$$\forall h\in\mathcal{H} \quad L_{\mathcal{D}}(h)\leq L_S(h)+\epsilon_{\nu(h)}(m,\omega(\nu(h))\cdot\delta) \text{.}$$

We have fixed the sample complexity and the weights. Now we want to find a hypothesis minimising the true error with respect to those parameters.

Structural Risk Minimiser: Pick $$h\in \text{argmin}_{h\in\mathcal{H}}\{L_S(h)+\epsilon_{\nu(h)}(m,\omega(\nu(h))\cdot\delta)\}$$.

To obtain nonuniform learnability we can pick a hypothesis $\tilde{h}\in\mathcal{H}$ and choose our $\epsilon,\delta>0$ as usual. We then fix the sample complexity accordingly and apply the SRM paradigm.

Theorem: Let $$\mathcal{H}=\bigcup_{n\in\mathbb{N}}\mathcal{H}_n$$ where each $$\mathcal{H}_n$$ has the uniform convergence property. Then for any $$\tilde{h}\in\mathcal{H}$$ and any i.i.d. drawn sample set $$S\subset X$$ with $$|S|\geq m_{\mathcal{H}_{\nu(\tilde{h})}}^{UC}(\frac{\epsilon}{2},\omega(\nu(\tilde{h}))\cdot\delta)$$ we have with probability at least $$1-\delta$$ that
$$ L_{\mathcal{D}}(A(S))\leq L_{\mathcal{D}}(\tilde{h})+\epsilon \text{.}$$

Proof: Let $m\in\mathbb{N}$ be fixed. By the preceding theorem we have with probability at least $1-\delta$ that 

$L_{\mathcal{D}}(A(S))\leq\min_{h\in\mathcal{H}}(L_S(h)+\epsilon_{\nu(h)}(m,\omega(\nu(h))\cdot\delta))
\leq L_S(\tilde{h})+\epsilon_{\nu(\tilde{h})}(m,\omega(\nu(\tilde{h}))\cdot\delta)$.

Then with probability at least $1-\delta$ we have that

$L_{\mathcal{D}}(A(S))\leq L_S(\tilde{h})+\epsilon_{\nu(\tilde{h})}(m_{\mathcal{H}_{\nu(\tilde{h})}}(\frac{\epsilon}{2}, \omega(\nu(\tilde{h}))\cdot\delta),\omega(\nu(\tilde{h}))\cdot\delta)$

$\leq L_S(\tilde{h})+\frac{\epsilon}{2}$.

Since $\mathcal{H}_{\nu(\tilde{h})}$ has the uniform convergence property we have with probability at least $1-\delta$ that

$L_{\mathcal{D}}(A(S))\leq L_S(\tilde{h})+\frac{\epsilon}{2}\leq L_{\mathcal{D}}(\tilde{h})+\frac{\epsilon}{2}+\frac{\epsilon}{2}=L_{\mathcal{D}}(\tilde{h})+\epsilon$.

A more general formulation of this result is the following.

Corollary: If $\mathcal{H}=\bigcup_{n\in\mathbb{N}}\mathcal{H}_n$ where each $\mathcal{H}_n$ is PAC-learnable, then $\mathcal{H}$ is nonuniformly learnable.

The statement of the corollary is actually an equivalence. This is shown in another entry of this wiki. Furthermore there is an entry comparing the different notions of learnability and their usefulness in practice.
