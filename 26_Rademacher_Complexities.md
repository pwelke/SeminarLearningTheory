---
title: "Chapter 26: Rademacher Complexities"
---

# Rademacher Complexities

In chapter 4 it has been shown that the property of uniform convergence implies learnability and that the ERM-rule is $\epsilon$-consistent.

In this chapter Rademacher Complexity is introduced which measures the rate of uniform convergence.

#### Notation:

At first some notation is defined. Given a fixed loss function $\mathcal{l}$ and a hypothesis class $\mathcal{H}$ we define the set of all the projection from a sample to its loss for the hypothesis class $\mathcal{H}$ as

$\mathcal{F} := \mathcal{l} \circ \mathcal{H} := \\{z \mapsto \mathcal{l}(h,z) :h \in \mathcal{H} \\} $.

Given some $f \in \mathcal{F} $ define the loss of $f$ over the whole distriburion 

$\mathcal{L}\_D := \mathbb{E}\_{z \sim \mathcal{D}} \[ f(z) \] $

and the lossof $f$ over a sample as 

$\mathcal{L}\_S := \frac{1}{m} \sum \_{i=1}^m f(z_i)$.

Finally, define $\mathcal{F} \circ S$ as the set of all possible evaluations a function $f ∈ \mathcal{F}$ can achieve on a sample $S$:

$\mathcal{F} \circ S := \\{(f(z_1), \dots,f (z_m)) :f\in \mathcal{F}\\}$

#### Definitions:

The **Representativeness of S with respect to F** is defined as

$\mathcal{Rep}\_{\mathcal{D}} (\mathcal{F},S) := \sup_{f\in\mathcal{F}} (\mathcal{L}\_\mathcal{D} (f) − \mathcal{L}\_S (f))$.

It measures the biggest difference between the losses measured in the sample $S$ and over the whole set.

In general it is not possible to calculate the loss of an hypothesis over the whole domain and in practice the representativeness is estimated by splitting up the sample S in some training and validation set.

FOTO

The **Rademacher Complexity** does exactly this, by splitting up the sample $S$ in all possible combination of training and validation set.

$\mathcal{R}(\mathcal{F} \circ S) := \frac{1}{m}  \mathop{\mathbb{E}}\_{\sigma \sim \\{\pm 1\\}^m } \[ \sup \_{f \in \mathcal{F} } \sum_{i=1}^{m} \sigma_i f ( z_i ) \] $

The definition makes use of $\sigma \sim \\{\pm 1\\}^m$ assigning a sample either to the training or validation set where $\sigma$ i.i.d. with $\mathbb{P}\[ \sigma_i = 1\] = \mathbb{P} \[ \sigma_i = − 1\]  = \frac{1}{2} $.

#### Lemmas and Theorems:

The first Lemma 26.2 that is shown bounds the expected value of representativeness of S by twice the expected Rademacher Complexity.

$ \mathop{\mathbb{E}} \_{S \sim \mathcal{D}^m} \[ \mathcal{Rep}\_\mathcal{D} (F,S )] 
\leq 
2 \mathop{\mathbb{E}} \_{S \sim \mathcal{D}^m}  \mathcal{R} ( \mathcal{F} \circ S) $

This implies that by splitting up the sample $S$ into different validation and training sets one can actually estimate the (expected value of the) loss difference between sample $S$ and the distribution $\mathcal{D}$. 

Lemma 26.2 can be applied directly to the Representativeness of a specific hypothesis, for example $ERM_\mathcal{H}(S)$ or some $h^\*$ (Theorem 26.3).

In general, we want to bound the expected value of the representaticeness of $S$ with a better dependence on the confidence parameter $\delta \in (0,1)$.
This is achieved by applying the McDiarmid's Inequality. 

For  all samples $z$ and $h \in \mathcal{H}$  their loss needs to be bounded by a constant $\| \mathcal{l} ( h,z ) \| \leq c$.

Then, 

**(i)**  With probability of at least $1 − \delta$, for all $h \in \mathcal{H}$, 

$\mathcal{L}\_\mathcal{D} (h) − \mathcal{L}\_S (h) \leq 2 \mathop{\mathbb{E}} \_{S' \sim \mathcal{D}^m} \mathcal{R} ( \mathcal{l} \circ \mathcal{H} \circ S' ) + c \sqrt{ \frac{2 ln(\frac{2}{\delta})}{m} }$ .


In particular, this holds for $h = \text{ERM}\_\mathcal{H} ( S )$ .

**(ii)**  With probability of at least $1 − \delta$, for all $h \in \mathcal{H}$, 

$\mathcal{L}\_\mathcal{D} (h) − \mathcal{L}\_S (h) \leq 2 \mathcal{R} ( \mathcal{l} \circ \mathcal{H} \circ S)  + 4 c \sqrt{ \frac{2 ln(\frac{4}{\delta})}{m} } $.
 
In particular, this holds for $h = \text{ERM}\_\mathcal{H} ( S )$.

**(iii)**  For any $h^\*$, with probability of at least $1 − \delta$, 

$\mathcal{L}\_\mathcal{D} ( \text{ERM}\_\mathcal{H} ( S ) ) − \mathcal{L}\_\mathcal{D} (h^\*) \leq 2
\mathcal{R} ( \mathcal{l} \circ \mathcal{H} \circ S) + 5 c \sqrt{ \frac{2 ln(\frac{8}{\delta})}{m} } $.

Theorem 26.5 gives three different bounds that mainly say, that, if the Rademacher Complexity $\mathcal{R}(\mathcal{l} \circ \mathcal{H} \circ S)$ is small, the ERM-rule can be used.
Also the second and third bound depend on the chosen training sample $S$, which is called a data-dependent bound and in comparison to other bounds, the third **bound can be calculated**!

#### Rademacher Calculus:

Four Properties where proven for the Rademacher Calculus which can be applied to bound the Rademacher Complexity \mathcal{R}(\mathcal{l} \circ \mathcal{H} \circ S)$ for specific cases.

For a set $A$ in $\mathbb{R}^m$
1. When applying an affine transformation with factor $c \in \mathbb{R}$ and translation $a_0 \in \mathbb{R}^m$ to A, it holds 
$\mathcal{R}({ca + a_0 : a \in A }) \leq \| c \| \mathcal{R} (A) $
2. The Rademacher Complexity of the complex hull of $A$ is equal to the Rademacher Complexity of $A$
3. Massart-Lemma: The Rademacher Complexity of a finite set grows logarithmically with its size.
4. Contraction Lemma: If in every dimension $i \in \[m\]$ of $A$ a $\rho$-Lipschitz function $\varphi_i:\mathbb{R} \to \mathbb{R}$ is applied the Rademacher complexity of the transformed $\Phi(A)$ can be bounded via 
$\mathcal{R}(\Phi(A)) \leq \rho \mathcal{R}(A)$.

#### Rademacher Complexity of Linear Classes:

The following two linear and bounded hypothesis classes will be analyzed in detail applying some of the properties for Rademacher Calculus:

$\mahtcal{H}\_1 = \{ x \mapsto \langle w , x \rangle : \\| w \\|\_1 \leq 1 \}$

$\mahtcal{H}\_2 = \{ x \mapsto \langle w , x \rangle : \\| w \\|\_2 \leq 1 \}$

The hypothesis class $\mahtcal{H}\_2$ can be bounded by the maximum $\mathcal{l}\_2$-norm of a sample from Hilbert space $S$ devided by the square root of $m$, the size of $S$. Notice that the dimension of the Hilbert space $S$ does not influence the Rademacher complexity \mathcal{R}(\mathcal{l} \circ \mathcal{H}\_2 \circ S)$, which is usefull when analyzing kernel methods.

A similar bound can be proven for $\mahtcal{H}\_1$, but the dimension of $S$ does appear in the numerator of the bound.

The two Lemmata imply two generalization bounds.

---

### Questions:

**Q:** On the page 376 the very first line $\sigma$ is introduced. Should the distribution of 
-1 and +1 be equal?

**A:** Yes, since we further assume that the sizes of two disjoint sets are equal. 

___

**Q:** Page 378. Formula on the top of the page. Would it suffice if $h^*$ **(???)** is Lipschitz continuous?

**A:** Yes, but we have to bound something. (for Lipschitz - domain). 

___

**Observation:** Theorem 26.5 - 3. is a remarkable result: if we learn our S, 
we have learnt the overall distribution pretty much.


___

**Q:** Lemma 26.8 - why do they use maximum of differences between estimated and actual $a$?

**A:** They use the geometric idea of difference between mean and center, where center is an actual $a$.


___

**Q:** Lemma 26.10 - why does not hold for $\mathcal{H}_1$?

**A:** The $\mathcal{v}$ can be bounded by whatever.


___

**Q:** Can we use $\mathcal{l}_1$-norm for kernel methods?

**A:** **No** there is dimension under the square root. 


___

**Q:** Theorem 26.13 bounds probability of misclassification. 
Why do they use $\mathcal{R}$-value in statement and not in the proof?

**A:** Value $\mathcal{c}$ which was used previously (for example in Theorem 26.12) 
in front of the square root is bounded by this $\mathcal{R}$-value.
