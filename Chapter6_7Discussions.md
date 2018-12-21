# Questions:
**Q:**
Why is the definition of $\mathcal{H}\_0$ and $\mathcal{H}\_1$ not exclusive?

**A:**
As we want to have $\|\mathcal{H}\_S\| = \mathcal{H}\_0 + \mathcal{H}\_0$, we have to count all the hypothesis,  where "and" is true, twice.

**Q:**
Why we use the term "convergence"?

**A:**
We use the term convergence in the calculus limit sense, as we can get $L\_S(h)$ arbitrarily close to $L\_{\mathcal{D}}(h)$ with a large enough sample size.

**Q:**
Is the $min$ in the definition of $\epsilon\_n$ a problem?

**A:** (parial)
An $inf$ instead of $min$ should be more appropriate, as  $\epsilon\_n$ could converge to 0 or $\epsilon\_n=0$ could happen. But if we would use the $inf$ and therefore allow $\epsilon\_n=0$ we would get problems in later proofs, as we sometimes divide by $\epsilon\_n$. 

**Q:**
What is the meaning of the weight function wrt. regularization?

**A:**
Basic idea is to use some prior knowledge of the $\mathcal{H}\_n$ to define the weight function. In that way, we can enforce a regularization during the learning to prefer more *simpler* solutions.