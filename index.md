---
title: Home
---

# Accompanying Wiki for the Seminar on Learning Theory

The wiki of this repository is used for the written documentation of the Seminar Principles of Data Mining and Learning Algorithms – „Learning Theory“ MA-INF 4209, taught at the University of Bonn during the Winter Termin 2018/2019 by Pascal Welke & Michael Kamp.

## Table of Contents

{% for p in site.pages %}
1) [{{ p.title }}]({{site.baseurl}}{{ p.url }})
{% endfor %}

