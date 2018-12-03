---
layout: home
image:
  feature: blackboard_large.jpg
permalink: /
title: " "
---


<img style="float: left; padding-right:50px;" src="images/jnattila_small.jpg">

# [About me](/about)

I am a researcher working on fields like relativistic astrophysics and computational physics focusing mainly on compact objects like neutron stars and black holes. For this I use tools such as pen & paper and supercomputers.

I am a Nordita Fellow in [Nordic Institute for Theoretical Physics](http://www.nordita.org) (Nordita, Stockholm, Sweden). I am also an avid open-source science & software advocate so you can find my research and codes freely [available](https://github.com/natj).

### Research 

I have a wide range of interdisciplinary research interests. Mostly I, however, like to focus on computational astrophysics. <!-- I enjoy working on projects that identify ''*first order*'' principles and make connections between other fields of physics and sciences. -->


<div class="inforow">
<div class="infocolumn" markdown="block">
- **High-energy astrophysics**: accretion (accretion disks); compact objects (neutron stars, black holes)
- **Plasma physics**: collisionless plasma dynamics; turbulence; particle acceleration
</div>
<div class="infocolumn" markdown="block">
- **Nuclear physics**: equation of state of cold ultra-dense neutron matter
- **General relativity**: ray tracing
- **Statistics**: Bayesian inference; Monte Carlo methods
</div>
<div class="infocolumn" markdown="block">
- **Computer sciences**: high performance computing; parallellization paradigms; machine learning; Julia language
- **Mathematics**: cellular automata models; topology
</div>
</div> <!-- /.inforow -->

---

## Recent publications & blog posts

<div class="tiles">
{% for post in site.posts limit:16 %}
   {% if post.title != empty %}	
	{% include post-grid.html %}
   {% endif %}
{% endfor %}
</div><!-- /.tiles -->

<div style="float:right" markdown="block">
#### For more posts see [publications](/articles) and [other posts](/projects).
</div>


