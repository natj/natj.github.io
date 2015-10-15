---
layout: home
image:
  feature: blackboard_large.jpg
permalink: /
title: " "
---


<div class="tiles">

{% for post in site.categories.info %}
  {% include post-grid-highlight.html %}
{% endfor %}

{% for post in site.posts %}
   {% if post.title != empty %}	
	{% include post-grid.html %}
   {% endif %}
{% endfor %}

</div><!-- /.tiles -->