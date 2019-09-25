---
layout: home
image:
  feature: blackboard_large.jpg
permalink: /
title: " "
---

<img style="float: left; padding-right:50px;" src="images/jnattila_small.jpg">



# [About me](/about)



I am an astrophysicist focusing on topics like cosmic plasmas, high-energy astrophysical phenomena, and computational physics.
I've also done some research on computer sciences, statistics, and machine learning.
For this I use tools such as pen & paper and supercomputers.

From 2020 I'll start as a Flatiron Research Fellow in [CCA/Flatiron](https://www.simonsfoundation.org/flatiron/center-for-computational-astrophysics/) and Columbia University, (New York, USA).
Previously, I was a Nordita Fellow in [Nordic Institute for Theoretical Physics](http://www.nordita.org) (Stockholm, Sweden). 
I am also an avid open-source science & software advocate --- you can find my research and codes freely available from [GitHub](https://github.com/natj).


### Research 

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
<h4 style="margin-top: 0.2em; margin-bottom: 0.0em;"> Notes on physics (work-in-progress)</h4>
Most of these research notes are done in connection to some publication. If you want to cite these, let me know and I'll point you to right a paper.

- [Relativistic plasma physics](https://github.com/natj/notes-corpus/blob/master/plasma-physics/notes.pdf)
- [Digital filtering](https://github.com/natj/notes-corpus/blob/master/filtering/notes.pdf)
- [Introduction to neutron star](https://github.com/natj/thesis) (my PhD thesis)


#### Teaching

- [CSC High-performance Summer School](https://www.csc.fi/en/web/training/-/csc_summerschool_2019)
    - latest materials from [2019](https://github.com/csc-training/summerschool)
- [Introduction to Julia](https://github.com/csc-training/julia-introduction) (CSC)
- [Introduction to UNIX](https://github.com/natj/unix-intro) (Univ. Turku)
- [Scientific writing tips](https://github.com/natj/sci_writing)
</div>
<div class="infocolumnR" markdown="block">
<h4 style="margin-top: 0.2em; margin-bottom: 0.0em;"> Undergraduate/PhD collaborators</h4>

- Tuomo Salmi (host for Nordita PhD visit; MSc and BSc thesis co-supervisor)
- Maarja Bussov (host for Nordita PhD visit)
- John Hope (MSc thesis supervisor)
- [Jere Kuuttila](https://www.mpa-garching.mpg.de/person/54672/2377) (MSc thesis co-supervisor)
- Eemeli Annala (PhD collaboration)

<h4 style="margin-top: 0.2em; margin-bottom: 0.0em;"> Senior collaborators </h4>

- Pavel Abolmasov
- [Axel Brandenburg](https://www.nordita.org/~brandenb/) (Nordita)
- [Andrei Beloborodov](https://physics.columbia.edu/people/profile/398) (Columbia Univ.)
- [Tyler Gorda](http://www.phys.virginia.edu/People/personal.asp?UID=tdg5cs) (Univ. Virginia)
- Jari Kajava (Univ. Turku)
- [Aleksi Kurkela](https://th-dep.web.cern.ch/roster/kurkela-aleksi) (CERN)
- [Cole Miller](https://www.astro.umd.edu/~miller/) (Univ. Maryland)
- [Farrukh Nauman](https://fnauman.github.io/) (Chalmers U.)
- [Pauli Pihajoki](https://blogs.helsinki.fi/pihajoki/) (Univ. Helsinki)
- [Juri Poutanen](http://users.utu.fi/jurpou/) (Univ. Turku/Tuorla Observatory)
- [Lorenzo Sironi](http://user.astro.columbia.edu/~lsironi/Site/Home.html) (Columbia Univ.)
- [Andrew Steiner](http://neutronstars.utk.edu/) (Univ. Tennessee / ORNL)
- Valery Suleimanov (Univ. Tubingen)
- [Aleksi Vuorinen](https://www.mv.helsinki.fi/home/arjvuori/) (Univ. Helsinki)
- Alexandra Veledina (Nordita / Univ. Turku)
</div>
</div> <!-- /.inforow -->


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


