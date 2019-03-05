# No-Free-Lunch Theorem

Whenever we choose a hypothesis class $\mathcal{H}$, we actually make use of some prior knowledge about our data. We only choose the class because we believe (or hope) that it contains a good (i.e. low-error) estimator for the concept we want to learn.
This begs the question whether such prior knowledge is a necessary condition for learning, or whether there can exist a "universal learner''. Recall that a learning task is defined by an unknown probability distribution $\mathcal{D}$ over the set of all possible examples and labellings $\mathcal{X}\times \mathcal{Y}$, and given a training set of size $m$, we want to find a hypothesis $h$ that has a low error with high probability. So a universal learner would correspond to an algorithm $A$ and a sample complexity $m$ such that $A$ finds a low risk predictor $h$ for *every* distribution $\mathcal{D}$ with high probability. The following theorem effectively states that no such learner can exist.

  

## The No-Free-Lunch Theorem

Let us first review the formal statement of the theorem.

**No-Free-Lunch Theorem**

Let $A$ be any learning algorithm (for binary classification with regards to the $0-1$ loss) over the domain $\mathcal{X}$. Let $m < \|\mathcal{X}\|/2$ be the size of a training set. Then there exists a distribution $\mathcal{D}$ over $\mathcal{X}\times \lbrace 0,1 \rbrace$ such that:

1. There exists a function $f : \mathcal{X} \to \lbrace 0,1 \rbrace$ with $L_{\mathcal{D}}(f) = 0.$

2. With probability of at least $1/7$ over the choice of $S \sim \mathcal{D}^{m}$ we have that $L_{\mathcal{D}}(A(S)) \geq 1/8$.

Recall that PAC-learnability requires that there is an algorithm $A$ and a sample complexity $m(\epsilon,\delta)$ for any $\epsilon>0$, $0<\delta<1$, such that $L_{\mathcal{D}}(A(S)) \leq \epsilon$ with probability at least $1-\delta$. 
The above theorem tells us that, if we do not restrict ourselves to a subset of all functions from $\mathcal{X}$ to $\lbrace 0,1 \rbrace$ (i.e. choose a hypothesis space), there will always be a probability distribution that makes any learning algorithm return a "bad'' predictor with high probability, even though there exists one with zero error. This implies that no algorithm will be able to PAC-learn this target concept.

In the following, the main idea of the proof will be pointed out, as it plays a role in pointing out the motivation behind the VC-Dimension.

### Proof (sketch): ### 

The basic idea is to take a set $C \subset \mathcal{X}$ of size $2m$ and then define a distribution for each possible function from $C$ to $\lbrace 0,1 \rbrace$ that forces our learner to output a bad hypothesis with high probability.
There are $T = 2^{2m}$ such functions $f_{1},...,f_{T}$. For each $f_{i}$, define a distribution $\mathcal{D}_{i}$ in the following way:

$\mathcal{D}\_{i}(\lbrace x,y \rbrace ) = 1/|C|$ if  $y = f_{i}(x)$, and
$\mathcal{D}\_{i}(\lbrace x,y \rbrace ) = 0$ otherwise.

So the samples that $f_{i}$ would classify correctly are uniformly sampled with probability $1/\|C\|$, while all other samples have probability 0. This way we can guarantee that for each $\mathcal{D}\_{i}$ there exists a zero-error hypothesis, namely $f_{i}$. It can then be shown that 

$\max_{i\in [T]} E_{S\sim\mathcal{D}^{m}} [L_{\mathcal{D}}(A'(S))] \geq 1/4,$

which implies the claim (can easily be shown using Markov's inequality).

### Consequences ###

As a direct consequence if follows that, for some infinite domain $\mathcal{X}$, the set of all functions from $\mathcal{X}$ to $\lbrace 0,1 \rbrace$ cannot be PAC-learnable. No matter what training set size $m$ we pick, $\|\mathcal{X}\|$ will always be larger than $2m$. So we can always apply the above theorem.

One way to tackle this problem is the choice of a suitable hypothesis class. This usually restricts the set of functions to choose from. The proof of the No-Free-Lunch Theorem only works because we are considering all possible functions from our domain to $\lbrace 0,1 \rbrace$. So restricting ourselves may indeed exclude such unfavourable distributions that prohibit PAC-learning.
