---
title: "Chap. 1&2"
---

## Introduction & a Gentle Start

The main goal of the book is to provide statistical learning theory for *supervised*, *passive* *batch* learning from *random* training data. For that, the following formal notation is used.
* domain set $\mathcal{X}$, instance $x\in\mathcal{X}$

* label set $\mathcal{Y}$, label $y\in\mathcal{Y}$

* training data $S&space;=&space;\left((x_1,y_1),\dots,(x_m,y_m)&space;\right&space;)&space;\in\left(\mathcal{X}\times\mathcal{Y}&space;\right&space;)^m$

* hypothesis $h\!:\mathcal{X}\to\mathcal{Y}$
* (unknown) data generator model $f\!:\mathcal{X}\to\mathcal{Y}$ and input distribution $\mathcal{D}\!:\mathcal{X}\to[0,1]$

* measure of success: **risk** or generalization error $\mathcal{L}_{\mathcal{D},f}(h):=P_{x\sim\mathcal{D}}\left[h(x)\neq&space;f(x)&space;\right&space;]$


### Empirical Risk Minimization
* restrict search space to hypothesis class $\mathcal{H}$

* **empirical risk** $\mathcal{L}_S:=\frac{1}{m}\left|&space;\left\{&space;i\in&space;[m]:&space;h(x_i)\neq&space;f(x_i)\right\}\right|$ for training set $S$

* define ERM as $h_S&space;=&space;ERM_\mathcal{H}(S)&space;=&space;\arg\min_{h\in\mathcal{H}}\mathcal{L}_S(h)$

  * inductive bias through restriction on $\mathcal{H}$

  
### Generalization Bound for ERM in a Restricted Case
For the following result, three assumptions are made:
* $\mathcal{H}$ is finite
* realizability, i.e., $\exisits&space;h^*\in\mathcal{H}\&space;\&space;s.t.\&space;\&space;\mathcal{L}_{\mathcal{D},f}(h^*)=0$

  * note that from this follows that the empirical risk is 0 for all but negligible many S
* iid training data, i.e., $draw\&space;x_i\in&space;S&space;iid&space;from&space;\mathcal{D},\&space;set\&space;y_i=f(x_i)$


With this, the following generalization bound can be given:

**Corollary:** 

$finite\&space;\mathcal{H},\delta\in&space;(0,1),&space;\epsilon&space;>0,&space;m\geq\frac{\log\frac{|\mathcal{H}|}{\delta}}{\epsilon}$


$\Rightarrow&space;\forall&space;\mathcal{D},f\&space;realizable,\&space;with\&space;prob.\&space;1-\delta\&space;for\&space;iid\&space;sample\&space;S\&space;of\&space;size\&space;m,&space;h_S=ERM_\mathcal{H}(S)\&space;it\&space;holds\&space;that$


$\mathcal{L}_{\mathcal{D},f}(h_S)\leq\epsilon$



### Questions:
1. When calculating the error of an hypothesis why do we compare the error of the obtained hypothesis with $$h^{*}$$
 (in hypothesis space $$\mathcal{H}$$
) and not with $$f$$
? 

In general we compare results with $$h^{*}$$
, because given the hypothesis space $$\mathcal{H}$$
 it is the result closest to the real function one could possibly obtain.

2. Is it possible to calculate $$h^{*}$$
?

3. In the sample set $$S$$
 are duplicates of instances allowed? And what is the actual influence of duplicats in sample $$S$$
?

Yes, duplicates are allowed because the instances are i.i.d. and therefore it is possible.
In practical apoaches duplicates in the sample set are very rare. Nevertheless, the algorithm should be prepared for this case since some methods could break, for example an inversion of a matrix because of singularity.

4. In the proof of the Corollary where do we use the assumption on realizability?

We utilize the assumption when assuming there exists an hypothesis with $$\mathcal{L}_{S}(h)=0$$
.

5. Why $$\varepsilon>0$$
 and not $$\varepsilon&space;\in&space;[0,1]$$
 since it is a probability?

Later on epsilon could be the value of a loss function and considering $$\varepsilon>0$$
 one can apply the corollary.

6. Would anyone ever calculate m utilizing the corollary?

For legal bounds for example in medicine being able to calculate a probability of an error is very important. Of cause the realizability assumption is very strong. Later on we are going to see a similar corollary without the assumption.

7. Is the upper bound in the corollary a sharp bound?

Sometimes the considered bounds are right but generally one can only proof uper and lower bounds.

8. The goal utilizing ERM is always to minimize the risk oder the input space. Rare cases (with respect to distribution $$\mathcal{D}$$
) are not considered because they have a very low probabilty but especially those rare cases (for example the corner case in autonomous driving) are the ones that are most interesting because of their strong impacts. How can the algorithms be good on those rare cases?

ERM sadly doesn't work very well for those cases. But there are practical solutions for example
- to overdistribute the rare examples by hand or
- change the loss function. A bad outcome is asigned a very high value by the error function.

9. Having a machine that is very conservative in risk taking and tends to overestimate errors could be problematic. So a quite philosophical question is what is better: overestimate or underestimate the error?

10. What is overfitting?

