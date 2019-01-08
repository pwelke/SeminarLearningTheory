# Addition to VC-Dimensions

In this section we pick up the topic of VC-dimensions again, adding some technical but famous results. In particular we present Sauer's Lemma and (without a proof) one of its applications. We will also define a way to analyse the expressive power of a hypothesis space.


Remark: Let in the following $\mathcal{H}$ be a hypothesis space on a domain $X$, where $X$ is given an arbitrary probability distribution $\mathcal{D}$.


Definition:
We define the restriction of $\mathcal{H}$ to a sample set $S\subset X$ as 
$$ \mathcal{H}_S := \{h|_S : S \rightarrow \{ 0,1\} : h \in \mathcal{H} \}\text{.} $$


Definition:
We define the growth function of $\mathcal{H}$ as 
$$ \tau_{\mathcal{H}}: \mathbb{N}\rightarrow\mathbb{N}\text{,} \quad \tau_{\mathcal{H}}(m) := \max_{S\subset X\text{,} \ |S|=m} |\mathcal{H}_S|\text{.}$$


The growth function tells us how the expressive power of the hypothesis spaces evolves when enlarging the sample size. If it grows exponentially, $\mathcal{H}$ is very general. On the other hand, if $\tau_{\mathcal{H}}$ is eventually constant, we have a clearly restricted hypothesis space.  A very famous result is Sauer's Lemma which bounds the growth function with respect to the VC-dimension.


Lemma (Sauer et al.):
Let $VCdim(\mathcal{H}) \leq d < \infty $. Then 
$$ \tau_{\mathcal{H}}(m)\leq \sum^d_{i=0} \binom{m}{i}$$ for all $m\in \mathbb{N}$.

Proof: First we observe that for any $S\subset X$ 
$$|\{ B\subset S: \mathcal{H} \ shatters \ B \}| \leq \sum^d_{i=0} \binom{|S|}{i}\text{,}$$ since no set of size $>d$ can be shattered and $S$ contains $\binom{\|S\|}{i}$ subsets of size $i$.

Claim: $\|\mathcal{H}_S\|\leq \|\{ B\subset S: \mathcal{H} \ shatters \ B\}\|$.

Proof of the claim: Proof by induction on the sample complexity of $S$.

$\|S\|= 1$: The empty set is vacuously shattered. This leaves us with 
$$ |\mathcal{H}_S|= 1+ \Big\{^{1 \quad \text{if $S$ is shattered}}_{0 \quad \text{otherwise.}}$$
$1 <\|S\|$: Assume $\|S\|=m$ and $S=\{s_1, \dots, s_m\}$ for some $m\in\mathbb{N}$ and that the claim holds for sets of size $<m$. Let furthermore $S':= S\setminus \{s_m\}$. We define 

$ \mathcal{H}_0:= \{h\in\mathcal{H}_{S'}: h\cup (s_m,0)\in\mathcal{H}_S \vee h\cup(s_m,1)\in\mathcal{H}_S\}=\mathcal{H}_{S'}$,\\

$\mathcal{H}_1:=\{h\in\mathcal{H}_{S'}: h\cup (s_m,0)\in \mathcal{H}_S\wedge h\cup (s_m,1)\in\mathcal{H}_S\}$.

Note that for every $h\in\mathcal{H}_1\subset\mathcal{H}_0$ there is $\{h\cup(s_m,0), h\cup(s_m,1)\}\subset \mathcal{H}_S$. Hence $$\|\mathcal{H}_S\|=\|\mathcal{H}_0\setminus\mathcal{H}_1\|+2\|\mathcal{H}_1\|$$ and therefore $$\|\mathcal{H}_S\|=\|\mathcal{H}_0\|+\|\mathcal{H}_1\|\text{.}$$

We can apply the induction hypothesis on $\mathcal{H}_0$ and obtain 
$$ \|\mathcal{H}_0\|\leq\|\{ B\subset S': \mathcal{H} \ shatters \ B\}\|=\|\{ B\subset S: s_m \notin B\wedge \mathcal{H} \ shatters \ B\}\|\text{.}$$

For $\mathcal{H}_1$ we can construct a hypothesis space $\mathcal{H}'$ such that $\mathcal{H}_1=\mathcal{H}'_{S'}$. Namely, we define 
$$\mathcal{H}' := \{h\cup(s_m,0): h\in \mathcal{H}_1\}\cup\{h\cup (s_m,1): h\in\mathcal{H}_1\}\text{.}$$

We again apply the induction hypothesis 

$\|\mathcal{H}_1\|\leq \|\{B\subset S': \mathcal{H}' \ shatters \ B\}\|=\|\{B\subset S: s_m\in B \wedge \mathcal{H}' \ shatters \ B\}\|$

$=\|\{B\subset S: s_m\in B \wedge \mathcal{H} \ shatters \ B\}\|$.

Putting both inequalities together yields 
$$\|\mathcal{H}_S\|=\|\mathcal{H}_0\|+\|\mathcal{H}_1\|\leq \|\{B\subset S: \mathcal{H} \ shatters \ B\}\|\text{.}$$

This concludes the proof.


We now state without a proof an important theorem that puts the growth function into the context of learnability.


Theorem: Let $S\subset X$ be drawn i.i.d.. Then for every $\delta\in(0,1)$ we have with probability at least $1-\delta$ that
$$ \|L_{\mathcal{D}}(h)-L_S(h)\|\leq \frac{4\sqrt{\log{\tau_{\mathcal{H}}(2\|S\|)}}}{\delta\sqrt{2\|S\|}}\text{.}$$
