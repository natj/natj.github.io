---
layout: archive
title: "Projects"
excerpt: "A collection of my (scientific) projects and doodlings"
tags: []
image:
  feature:
  teaser:
---

<div class="tiles">
{% for post in site.categories.projects %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->