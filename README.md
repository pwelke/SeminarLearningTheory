# Accompanying Wiki for the Seminar on Learning Theory

The wiki of this repository is used for the written documentation of the Seminar Principles of Data Mining and Learning Algorithms – „Learning Theory“ MA-INF 4209, taught at the University of Bonn during the Winter Termin 2018/2019 by Pascal Welke & Michael Kamp.


## Introduction & a Gentle Start

The main goal of the book is to provide statistical learning theory for *supervised*, *passive* *batch* learning from *random* training data. For that, the following formal notation is used.
* domain set <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{X}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{X}" title="\mathcal{X}" /></a>, instance <a href="https://www.codecogs.com/eqnedit.php?latex=x\in\mathcal{X}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x\in\mathcal{X}" title="x\in\mathcal{X}" /></a>
* label set <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{Y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{Y}" title="\mathcal{Y}" /></a>, label <a href="https://www.codecogs.com/eqnedit.php?latex=y\in\mathcal{Y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y\in\mathcal{Y}" title="y\in\mathcal{Y}" /></a>
* training data <a href="https://www.codecogs.com/eqnedit.php?latex=S&space;=&space;\left((x_1,y_1),\dots,(x_m,y_m)&space;\right&space;)&space;\in\left(\mathcal{X}\times\mathcal{Y}&space;\right&space;)^m" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S&space;=&space;\left((x_1,y_1),\dots,(x_m,y_m)&space;\right&space;)&space;\in\left(\mathcal{X}\times\mathcal{Y}&space;\right&space;)^m" title="S = \left((x_1,y_1),\dots,(x_m,y_m) \right ) \in\left(\mathcal{X}\times\mathcal{Y} \right )^m" /></a>
* hypothesis <a href="https://www.codecogs.com/eqnedit.php?latex=h\!:\mathcal{X}\to\mathcal{Y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h\!:\mathcal{X}\to\mathcal{Y}" title="h\!:\mathcal{X}\to\mathcal{Y}" /></a>
* (unknown) data generator model <a href="https://www.codecogs.com/eqnedit.php?latex=f\!:\mathcal{X}\to\mathcal{Y}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f\!:\mathcal{X}\to\mathcal{Y}" title="f\!:\mathcal{X}\to\mathcal{Y}" /></a> and input distribution <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{D}\!:\mathcal{X}\to[0,1]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{D}\!:\mathcal{X}\to[0,1]" title="\mathcal{D}\!:\mathcal{X}\to[0,1]" /></a>
* measure of success: **risk** or generalization error <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{L}_{\mathcal{D},f}(h):=P_{x\sim\mathcal{D}}\left[h(x)\neq&space;f(x)&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{L}_{\mathcal{D},f}(h):=P_{x\sim\mathcal{D}}\left[h(x)\neq&space;f(x)&space;\right&space;]" title="\mathcal{L}_{\mathcal{D},f}(h):=P_{x\sim\mathcal{D}}\left[h(x)\neq f(x) \right ]" /></a>

###Empirical Risk Minimization
* restrict search space to hypothesis class <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}" title="\mathcal{H}" /></a>
* **empirical risk** <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{L}_S:=\frac{1}{m}\left|&space;\left\{&space;i\in&space;[m]:&space;h(x_i)\neq&space;f(x_i)\right\}\right|" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{L}_S:=\frac{1}{m}\left|&space;\left\{&space;i\in&space;[m]:&space;h(x_i)\neq&space;f(x_i)\right\}\right|" title="\mathcal{L}_S:=\frac{1}{m}\left| \left\{ i\in [m]: h(x_i)\neq f(x_i)\right\}\right|" /></a> for training set <a href="https://www.codecogs.com/eqnedit.php?latex=S" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S" title="S" /></a>
* define ERM as <a href="https://www.codecogs.com/eqnedit.php?latex=h_S&space;=&space;ERM_\mathcal{H}(S)&space;=&space;\arg\min_{h\in\mathcal{H}}\mathcal{L}_S(h)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_S&space;=&space;ERM_\mathcal{H}(S)&space;=&space;\arg\min_{h\in\mathcal{H}}\mathcal{L}_S(h)" title="h_S = ERM_\mathcal{H}(S) = \arg\min_{h\in\mathcal{H}}\mathcal{L}_S(h)" /></a>
  * inductive bias through restriction on <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}" title="\mathcal{H}" /></a>
  
###Generalization Bound for ERM in a Restricted Case
For the following result, three assumptions are made:
* <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{H}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{H}" title="\mathcal{H}" /></a> is finite
* realizability, i.e., <a href="https://www.codecogs.com/eqnedit.php?latex=\exisits&space;h^*\in\mathcal{H}\&space;\&space;s.t.\&space;\&space;\mathcal{L}_{\mathcal{D},f}(h^*)=0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\exisits&space;h^*\in\mathcal{H}\&space;\&space;s.t.\&space;\&space;\mathcal{L}_{\mathcal{D},f}(h^*)=0" title="\exisits h^*\in\mathcal{H}\ \ s.t.\ \ \mathcal{L}_{\mathcal{D},f}(h^*)=0" /></a>
  * note that from this follows that the empirical risk is 0 for all but negligible many S
* iid training data, i.e., <a href="https://www.codecogs.com/eqnedit.php?latex=draw\&space;x_i\in&space;S&space;iid&space;from&space;\mathcal{D},\&space;set\&space;y_i=f(x_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?draw\&space;x_i\in&space;S&space;iid&space;from&space;\mathcal{D},\&space;set\&space;y_i=f(x_i)" title="draw\ x_i\in S iid from \mathcal{D},\ set\ y_i=f(x_i)" /></a>

With this, the following generalization bound can be given:

**Corollary:** 

<a href="https://www.codecogs.com/eqnedit.php?latex=finite\&space;\mathcal{H},\delta\in&space;(0,1),&space;\epsilon&space;>0,&space;m\geq\frac{\log\frac{|\mathcal{H}|}{\delta}}{\epsilon}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?finite\&space;\mathcal{H},\delta\in&space;(0,1),&space;\epsilon&space;>0,&space;m\geq\frac{\log\frac{|\mathcal{H}|}{\delta}}{\epsilon}" title="finite\ \mathcal{H},\delta\in (0,1), \epsilon >0, m\geq\frac{\log\frac{|\mathcal{H}|}{\delta}}{\epsilon}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\Rightarrow&space;\forall&space;\mathcal{D},f\&space;realizable,\&space;with\&space;prob.\&space;1-\delta\&space;for\&space;iid\&space;sample\&space;S\&space;of\&space;size\&space;m,&space;h_S=ERM_\mathcal{H}(S)\&space;it\&space;holds\&space;that" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Rightarrow&space;\forall&space;\mathcal{D},f\&space;realizable,\&space;with\&space;prob.\&space;1-\delta\&space;for\&space;iid\&space;sample\&space;S\&space;of\&space;size\&space;m,&space;h_S=ERM_\mathcal{H}(S)\&space;it\&space;holds\&space;that" title="\Rightarrow \forall \mathcal{D},f\ realizable,\ with\ prob.\ 1-\delta\ for\ iid\ sample\ S\ of\ size\ m, h_S=ERM_\mathcal{H}(S)\ it\ holds\ that" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{L}_{\mathcal{D},f}(h_S)\leq\epsilon" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{L}_{\mathcal{D},f}(h_S)\leq\epsilon" title="\mathcal{L}_{\mathcal{D},f}(h_S)\leq\epsilon" /></a>


