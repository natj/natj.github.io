---
layout: home
image:
  feature: blackboard_large.jpg
permalink: /
title: " "
---

<div class="tiles">

<div class="tile">
  <a href="{{ site.url }}/about/" title="About me"><img src="{{site.url}}/images/jnattila_small.jpg" alt="teaser" itemprop="image"></a>
  <p class="post-excerpt">I am a graduate student at University of Turku, working on research fields like relativistic astrophysics and computational physics focusing on compact objects like neutron stars and black holes.</p>
</div><!-- /.tile -->

{% for post in site.posts %}
	{% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->