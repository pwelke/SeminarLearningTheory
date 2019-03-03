---
title: "Chap. 8"
---
# Runtime of Learning Algorithms
Usually, it is common to define the runtime of an algorithm in terms of the input size. But this naive definition is not directly applicable to learning problems. 

For example, defining the runtime in terms of the sample size may be complicated, as the algorithm could work with a much smaller subset of the input sample, which suffices for PAC learning, and solve the learning task in much less time. 

On the other hand, a dependence on $\epsilon$, $\delta$ and on a measure of the complexity of the learning task is preferable. 

Formally: 

**Computational Complexity of a Single Learning Task**

An algorithm $A$ solves a learning task $(Z, \mathcal{H}, l)$ in time $\mathcal{O}(f(\epsilon,\delta))$ if:
*  $A$ terminates in $\mathcal{O}(f(\epsilon,\delta))$ time.
*  $A$ accesses the data-generating distribution $\mathcal{D}$ at most $\mathcal{O}(f(\epsilon,\delta))$ time.
*  The output of $A$ is applicable to (new) instances in $\mathcal{O}(f(\epsilon,\delta))$ time. 
*  $A$  agnostically PAC learns $(Z, \mathcal{H}, l)$

$A$ solves the learning task $(Z, \mathcal{H}, l)$ efficiently if it solves the task in $\mathcal{O}(p(\frac{1}{\epsilon},\frac{1}{\delta}))$ time for some polynomial $p$.

We want to generalize these notions to a sequence of learning tasks $(Z\_n, \mathcal{H}\_n, l\_n)\_{n=1}^\infty$, as we often have the situation, that $A$ can solve the learning task efficiently for each fixed $n$, but not in general: 

**Computational Complexity of a Sequence of Learning Tasks**
An algorithm $A$ solves a sequence of learning tasks $(Z\_n, \mathcal{H}\_n, l\_n)\_{n=1}^\infty$ in time $\mathcal{O}(f\_n(\epsilon,\delta))$ if:
*  For each fixed $n$, $A$ solves the learning task $(Z, \mathcal{H}, l)$ in time $\mathcal{O}(f\_n(\epsilon,\delta))$

$A$ solves the learning task $(Z\_n, \mathcal{H}\_n, l\_n)\_{n=1}^\infty$ efficiently, if it solves the task in $\mathcal{O}(p(\frac{1}{\epsilon},\frac{1}{\delta},n))$ time for some polynomial $p$.

## Examples
The following examples show that for general hypothesis classes efficient learning is hard. Still, for certain hypothesis classes, some tricks, like assuming realizability or solving the task representation independently, allow us to solve the task efficiently.
### Axis-aligned Rectangles (Realizable Case)
![Realizable Rectangle](https://github.com/pwelke/SeminarLearningTheory/raw/master/images/rectangle%20realizable.png)

In this problem, we have given a set of binary labelled points in $\mathbb{R}^n$ and $\mathcal{H}\_n$ is the set of axis-aligned rectangles in $\mathbb{R}^n$. One possible way to solve this learning task efficiently for a fixed $n$ is to first require a large enough number $m=m(\epsilon,\delta)=\mathcal{O}(p(\frac{1}{\epsilon},\frac{1}{\delta}))$ of samples to PAC-learn $\mathcal{H}\_n$. Secondly, we can determine for each dimension the smallest and largest coordinate of a positive instance. Those coordinates will correctly define an axis-aligned rectangle with zero empirical risk (i.e. an ERM hypothesis) efficiently in time $\mathcal{O}(nm)$.

So, this algorithm solves the learning task $(Z\_n, \mathcal{H}\_n, l\_n)\_{n=1}^\infty$ efficiently, but if $\mathcal{H}$ is the union of all $\mathcal{H}\_n$ this algorithm would not solve the learning task wrt. $\mathcal{H}$ efficiently, as the running time depends on $n$.

### Axis-aligned Rectangles (Agnostic Case)
![Realizable Rectangle](https://github.com/pwelke/SeminarLearningTheory/raw/master/images/rectangle%20agnostic.png)

Now, we slightly vary the problem, by allowing the samples to not come from an axis-aligned rectangle. Still, we want to find the rectangle with the lowest empirical risk. One can show, that it is NP-hard to compute an ERM rectangle in this setting, so we can not hope for an algorithm which efficiently solves this learning task. 

Nevertheless, for each fixed $n$ we can try out all subsets of size $2n$ of our $m$-sized sample, which defines an axis-aligned rectangle in $\mathbb{R}^n$ and will solve the task efficiently in time $\mathcal{O}(m^{\mathcal{O}(n)}).$

### Learning 3-Term-DNF Formulas
The following learning task is even NP-hard to learn in the realizable case:

The instance space $Z$ is the set of binary vectors $x \in \\{0,1\\}^n$ with a binary label. The hypothesis space $\mathcal{H}\_{3-t-DNF}$ is the set of so-called 3-term-DNF formulas. This is a disjunction of exactly three conjunctive terms $A\_1\lor A\_2 \lor A\_3$. 

### Learning 3-Term-DNF Formulas (Representation Independent)
One can check, that each 3-term-DNF formula can be rewritten as a 3-CNF formula of the form: $\bigwedge(a \lor b\lor c)$. 

If we allow the algorithm to representation independently learn $\mathcal{H}\_{3-t-DNF}$ (i.e. returning a hypothesis which is in general not a 3-term-DNF formula but only a 3-CNF) the problem becomes efficiently learnable.