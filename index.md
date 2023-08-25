---
layout: home
image:
  feature: turbulence.png
permalink: /
title: " "
---

<img style="float: left; padding-right:50px;" src="images/jnattila2.jpg">


# [About me](/about)

I am a computational astrophysicist studying high-energy astrophysical phenomena around neutron stars and black holes. For my research, I use both theoretical "pen-and-paper work" and large-scale supercomputer simulations.

I am currently a joint Flatiron Research Fellow in [Center for Computational Astrophysics, Flatiron Institute](https://www.simonsfoundation.org/flatiron/center-for-computational-astrophysics/) & Postdoctoral Reseacher in Columbia University (2020-2023; New York, USA). Before coming to New York, I was a Nordita Fellow in [Nordic Institute for Theoretical Physics](http://www.nordita.org) (2018-2020; Stockholm, Sweden). 

You can read more about my reserach [here](/about) and on [our group page](/group).


### In Finnish/Suomeksi:

Olen suomalainen astrofyysikko joka keskittyy suurenergia-astrofysiikan ääri-ilmiöiden tutkimiseen. Tutkin muun muuassa neutronitähtien purkauksia, pulsarien säteilyä, mustien aukkojen kertymäkiekkoja, sekä kosmisia radiopurskeita.


### [Research](/articles)

I have a wide range of interdisciplinary research interests. These reflect some of my latest publications:

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

<div class="inforow">

<div class="infocolumn2" markdown="block" style="background-color: #F0F0F0;">
<h4 style="margin-top: 0.2em; margin-bottom: 0.0em;"> Notes on physics</h4>

- [Relativistic plasma physics](https://github.com/natj/notes-corpus/blob/master/plasma-physics/notes.pdf)
- [MHD turbulence](https://github.com/natj/notes-corpus/blob/master/turbulence/notes.pdf)
- [Digital filtering](https://github.com/natj/notes-corpus/blob/master/filtering/notes.pdf)
- [Introduction to neutron stars](https://github.com/natj/thesis) (my PhD thesis)

Most of these research notes are done in connection to some publication. If you want to cite these, let me know and I'll point you to a right paper.

#### [Teaching](/teaching)

- [CSC High-performance Summer School](https://www.csc.fi/en/web/training/-/csc_summerschool_2019)
    - latest materials from [2019](https://github.com/csc-training/summerschool)
- [Introduction to Julia](https://github.com/csc-training/julia-introduction) (CSC)
- [Introduction to UNIX](https://github.com/natj/unix-intro) (Univ. Turku)
- [Scientific writing tips](https://github.com/natj/sci_writing)
</div>
<div class="infocolumnR" markdown="block">
<h4 style="margin-top: 0.2em; margin-bottom: 0.0em;"> Undergraduate/PhD collaborators</h4>

- Tuomo Salmi (host for Nordita PhD visit; MSc and BSc thesis co-supervisor)
- Maarja Kruuse (host for Nordita PhD visit)
- John Hope (MSc thesis supervisor)
- [Jere Kuuttila](https://www.mpa-garching.mpg.de/person/54672/2377) (MSc thesis co-supervisor)
- Eemeli Annala (PhD collaboration)

<h4 style="margin-top: 0.2em; margin-bottom: 0.0em;"> Senior collaborators </h4>

- [Axel Brandenburg](https://www.nordita.org/~brandenb/) (Nordita)
- [Andrei Beloborodov](https://physics.columbia.edu/people/profile/398) (Columbia Univ.)
- [James Cho](https://www.simonsfoundation.org/people/james-cho/) (Flatiron)
- [Aleksi Kurkela](https://th-dep.web.cern.ch/roster/kurkela-aleksi) (CERN)
- [Cole Miller](https://www.astro.umd.edu/~miller/) (Univ. Maryland)
- [Sasha Philippov](https://sashaphilippov.wixsite.com/sashaph) (Flatiron)
- [Juri Poutanen](http://users.utu.fi/jurpou/) (Univ. Turku)
- [Lorenzo Sironi](http://user.astro.columbia.edu/~lsironi/Site/Home.html) (Columbia Univ.)
- [Andrew Steiner](http://neutronstars.utk.edu/) (Univ. Tennessee & ORNL)
- Valery Suleimanov (Univ. Tubingen)
- [Aleksi Vuorinen](https://www.mv.helsinki.fi/home/arjvuori/) (Univ. Helsinki)
- Alexandra Veledina (Nordita & Univ. Turku)
</div>
</div> <!-- /.inforow -->


## Recent publications & blog posts

<div class="tiles">
{% for post in site.posts limit:32 %}
   {% if post.title != empty %}	
	{% include post-grid.html %}
   {% endif %}
{% endfor %}
</div><!-- /.tiles -->

<div style="float:right" markdown="block">
#### For more posts see [publications](/articles) and [other posts](/projects).
</div>


