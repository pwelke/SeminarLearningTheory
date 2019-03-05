---
title: "Chapter 5: Error Decomposition"
---

# Error Decomposition

From the No-Free-Lunch Theorem we can conclude that choosing a suitable hypothesis class is crucial for learning a given concept. This way we restrict ourselves to a subset of all possible functions from $\mathcal{X}$ to $\lbrace 0,1 \rbrace$, which helps us avoiding unfavourable distributions and might allow us to find a low-error hypothesis with high probability. On the other hand we might exclude the best hypotheses from our set of candidates, as it might not be a member of our hypothesis class. So we might find a good approximation for the best hypothesis in our class, but this best hypothesis in the class might be a bad approximation for the true target function. This dilemma is often referred to as the **Bias-Complexity Tradeoff** and shall be formalized in this section.
Recall the following definitions. If we choose a hypothesis class $\mathcal{H}$ and get a training set $S$ as input, we try to find a hypothesis $h_{S}$ minimizing the empirical risk $L_{\mathcal{D}}(h_{S})$. Now we can decompose the risk as follows:

$L_{\mathcal{D}}(h_{S}) = \epsilon_{app} + \epsilon_{est},$



where 

*  $\epsilon_{app} = \min_{h\in \mathcal{H}} L_{\mathcal{D}}(h)$ is the **approximation error**

* $\epsilon_{est} = L_{\mathcal{D}}(h_{S}) - \epsilon_{app}$ is the **estimation error**


The **estimation error** encodes how good our hypothesis performs in comparison to the best possible hypothesis in $\mathcal{H}$. It depends on the choice of $\mathcal{H}$ and the sample size $m$. The larger our samples, the better the expected performance of our empirical risk minimizer.

However, we have to take into account the **approximation error**. This tells us how the best hypothesis in $\mathcal{H}$ performs in comparison to the best overall hypothesis. Choosing a class where the best hypothesis is easy to approximate might therefore not be optimal, as it does not have to contain a good (i.e. low-risk) hypothesis at all. This error depends only on the hypothesis class chosen and not on the sample size.

The term tradeoff is used here because it is usually not possible to get both a low estimation and approximation error. If we choose $\mathcal{H}$ too large or complex (more on *complexity* of a hypothesis class under VC-Dimension), it might contain a good (or even optimal) hypothesis. But we might observe overfitting, i.e. the training error of our output hypothesis is low while its true error is rather large. On the other hand, if we choose a class where the training error is likely to be close to the true error, the hypotheses in $\mathcal{H}$ might not be potent enough to capture our target concept, which results in a large approximation error.
