---
title: "Errata"
---
# Errata

This section collects ideas for improvements of the book and errors we found. For each error, please specify the chapter and the exact location with a short description of the error or imprecision and an idea on how to improve the part.

## Chapter 1.1

Blah

## Chapter 3

1. On the page 46, the Bayes Optimal Predictor is discussed, but the proof of the claim about it is left for the exercise:
"see Exercise 7". Even though it is written, that it is "easy to verify", for the sake of understandability it would probably be better to show the proof.

2. For the definition of Agnostic PAC (page 46), explanation of the word "Agnostic" can probably can help readers to better 
understand the concept. For example: "Agnostic in this context means doubtful or uncertain about the existence of something".

3. The use case for the remark 3.2 (page 49) is not clear. Probably some clarification like "The "optimal" solution might be a bit outside of the hypothesis class. When it is impossible to find a solution within 
some constraints, it can be reasonable to relax those constraints. After relaxation, we are more likely to find a solution."

## Chapter 4

1. Remark 4.1 (page 57) The "Discretization Trick" is a bit ambiguous name for the idea, which is explained there, since there is no actual trick there,
but only the things, which we face in real life scenarios.

## Chapter 6

Lemma 6.1 on page 68 and Theorem 6.7 case 4 on page 72 miss the realisability assumption.

## Chapter 7

The epsilon function is defined on page 86 as

$$\epsilon_n: \mathbb{N}\times(0,1) \rightarrow (0,1), (m,\delta)\mapsto \min \{ \epsilon\in(0,1): m_{\mathcal{H}_n}^{UC}(\epsilon, \delta)\leq m \}$$.

Since we minimise over an open interval, the question arises whether this is always well-defined. Do we assume a "proper" agnostic case where $\epsilon =0$ never occurs? 


The definition of a prefix-free description language on page 89 is a little ambiguous since a "prefix" is not precisely defined. Is a string a prefix of itself? The addition of an injectivity assumption would clarify that.

## Chapter 26

Lemma 26.9 contains a typo: the last entry of $\phi(a)$ should be denoted $\phi_m(a_m)$ instead of $\phi_m(y_m)$.
