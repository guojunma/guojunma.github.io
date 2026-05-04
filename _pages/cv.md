---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* M.S. in Statistics, University of Victoria, 2023
* B.S. in Applied Mathematics,University of Alberta, 2020

Work experience
======
* Summer 2023: Research Assistant
  * University of Victoria
  * Supervisor: Professor Xuekui Zhang
  * Conducted a bioinformatics study to identify genomic regions associate with diseases.

* Sep. 2020 - Aug 2022 : Teaching Assistant
  * University of Victoria
  * Duties includes: Marking assignments and tutoring students.

* May 2021 - Aug 2021 : Data Analyst
  * IOTO International
  * Duties includes: Perform data collection, cleaning and analysis.


Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
Talks
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html  %}
  {% endfor %}</ul>
  
Teaching
======
  <ul>{% for post in site.teaching reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

Skills
======
* Statistical analysis: Bayesian statistics, design and analysis of experiment, time series analysis, generalized linear model, stochastic modelling, machine learning
* Computing: Python, R, SQL, Git & GitHub, Linux, High-Performance Computing (HPC), Genomic data analysis
* Languages: Mandarin, Cantonese, English

Service and leadership
======
* Organizing the local data-science reading group
