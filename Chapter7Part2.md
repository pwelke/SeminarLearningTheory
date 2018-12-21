---
title: "Chap. 7"
---




# Minimum Description Length (MDL) Principle and Occam's Razor
In this chapter we discuss the minimum description length principle as a spacial case of SRM and its philosophical analog the Occam's Razor.
## Minimum Description Length Principle
If we assume that $\mathcal{H}$ is countable, we can decompose it into singleton hypothesis classes:

$\mathcal{H} = \bigcup\_{n \in \mathbb{N}} \\{h\_n\\}.$

In this setting, we have: 

$n(h) = n$ 

By the known bound for finite hypothesis classes we get: 

$m^{UC}\_{\\{h\_n\\}} \leq log\left(\frac{\frac{2}{\delta}\|\\{h\_n\\}\|}{2\epsilon^2}\right) = log\left(\frac{\frac{2}{\delta}}{2\epsilon^2}\right)$

and $\epsilon\_n$ becomes: 

$\epsilon\_n(m,\delta) = \sqrt{\frac{log(\frac{2}{\delta})}{2m}}.$ 

To simplify notation, we can index the weights of a hypothesis not by $n$ as previously $w(n(h))$), but directly with $h$ as $w(h)$.
All together, the SRM rule becomes: 

$\boxed{\min\_{h \in \mathcal{H}} L\_S(h) + \sqrt{\frac{-log(w(h)) + log(\frac{2}{\delta})}{2m}}}$

### (Prefix Free) Description Languages
We want to use a special weighting scheme based on a *description language*:

* $\Sigma$: Finite alphabet (e.g. $\\{0,1\\}$) 
* $\Sigma^*$: All finite strings over $\Sigma$
* $d:\mathcal{H} \rightarrow \Sigma^{\*}$ *description language*
* $\|h\| := \|d(h)\|$ length of one string

We will need *prefix-free* languages:

$\forall h,h' \in \mathcal{H}, h \neq h': d(h) \text{ is not a prefix of } d(h').$

**Kraft Inquality**: $\mathcal{S}\subseteq \\{0,1\\}^*$ prefix free: 

$\sum\_{\sigma \in \mathcal{S}}\frac{1}{2^{\|\sigma\|}} \leq 1$ 

**Proof:**
Assume, we draw a binary sequence uniformly at random (and stop if it equals a string in $\mathcal{S}$). Then 

$\forall \sigma \in \mathcal{S}: P(\sigma) = \frac{1}{2^{\|\sigma\|}}.$

Overall, 

$\sum\_{\sigma \in \mathcal{S}}\frac{1}{2^{\|\sigma\|}} = P(\mathcal{S}) \leq 1.$

Due to Kraft inquality, we can use the description language $d(h)$ as a hypothesis weight $w(h) = \frac{1}{w^{\|h\|}}$.

If we plug $d(h)$ into the SRM rule for singleton hypothesis, we get the *Minimum Description Length* principle: 

$\boxed{\min\_{h \in \mathcal{H}}L\_S(h) + \sqrt{\frac{\|h\| + log(\frac{2}{\delta})}{2m}}}$

It can be seen as a tradeoff between the empirical risk of a hypothesis $L\_S(h)$ and the *complexity* of describing $h$.

## Occam's Razor
A philosophical view of MDL is the so called *Occam's Razor*: 

"A short explanation tends to be more valid than a long one"

# Constistency
Consistency is a notion even weaker than nonuniform learning. It allows the sample complexity to depend on the data generating distribution: 

Algorithm $A$ is *consistent* wrt. $\mathcal{H}$ and $\mathcal{P} = ($set of distributions$)$ if: 

$\exists \text{ function } m\_{\mathcal{H}}^{CON}:(0,1)^2\times\mathcal{H}\times\mathcal{P} \rightarrow \mathbb{N}$ s.t. 

$\forall \epsilon, \delta, \forall h \in \mathcal{H}, \forall \mathcal{D} \in \mathcal{P}$:

$\text{ for } S \text{ drawn i.i.d from } \mathcal{D}^m \text{ for } m \geq m\_{\mathcal{H}}^{CON}(\epsilon, \delta, h, \mathcal{D}):$ 

$L\_\mathcal{D}(A(S)) \leq L\_\mathcal{D}(h) + \epsilon$

## A Consistent Algorithm
Given an instance $x$, the algorithm Memorize returns the majority of known labels of instances in the sample $S$, which equal $x$. If there are no instances in $S$ equal to $x$ predict the majority of labels in $S$. It can be shown that this algorithm is consistent. 

This example makes it clear, that consistency is to weak to capture "learning" (or to be more precise: Generalization abilities).

# Comparison of Notions for Learning
The following tables compares the three different notions of learning in terms of bounds and prior knowledge.

| |  Bounds on the true error based on the empirical risk | Bounds on the quality of the output compared to the best hypothesis in the class  based on the sample size |  Encode prior knowledge |
| --- | --- | --- | --- |
| (agn.) PAC | $\checkmark$ | $\checkmark$ (in advance) | $\checkmark$ (by specifying an $\mathcal{H}$) | 
| Nonuniform | $\checkmark$ (e.g. Thm 7.4 in the book) | $\checkmark$ (depends on the best $h \in \mathcal{H}$) | $\checkmark$ (weights) |
| Consistent | $\times$ | $\times$ | $\times$ |



### Questions:
**Q:**

**A:**




