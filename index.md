---
layout: default
title: PhD Theses | AMASES
description: >-
  Discover PhD theses that have been written by scholars related to AMASES.
---

<a href="https://www.amases.org">
  <img src="assets/images/logo-AMASES.png"
       alt="A.M.A.S.E.S. – Associazione per la Matematica Applicata alle Scienze Economiche e Sociali"
       style="max-width: 100%; height: auto; display: block; margin: 0 auto 1.5em;">
</a>

<h1>PhD Theses</h1>

<p class="intro">
This is a list of {{ site.data.theses | size }} PhD theses in fields related to <a href="https://www.amases.org">AMASES</a> (Association for Mathematics
Applied to Economic and Social Sciences). It collects entries submitted by authors or supervisors, as well as all works archived by the <a href="https://tesidottorato.depositolegale.it">Biblioteca Centrale di Firenze</a> under the 2000 code for "Mathematical Methods for Economics, Finance, and Insurance". Titles are formatted according to language conventions: capitalized in English, lowercased in Italian or French.   
<br><br>
Requests for additions or corrections are welcome: just <a href="mailto:alessandra.cretarola@unich.it">email us</a>.
</p>

{% assign theses_by_year = site.data.theses | group_by: 'year' %}
{% assign theses_by_year_sorted = theses_by_year | sort: 'name' | reverse %}

<nav class="year-nav">
  {% for year in theses_by_year_sorted %}
    <a href="#{{ year.name }}">{{ year.name }}</a>
  {% endfor %}
</nav>

{% for year in theses_by_year_sorted %}
{% assign sorted_items = year.items | sort_natural: 'lastname' %}
<section id="{{ year.name }}">
  <h2 class="year-heading">{{ year.name }}</h2>
  <ul class="thesis-list">
    {% for thesis in sorted_items %}
    <li>
      <div class="thesis-author"><strong>{{ thesis.firstname }} {{ thesis.lastname }}</strong> ({{ thesis.affiliation }}, {{ thesis.year }})</div>
      <div class="thesis-title"><a href="{{ thesis.url }}" target="_blank" rel="noreferrer">{{ thesis.title }}</a></div>
      {% if thesis.supervisors and thesis.supervisors.size > 0 %}
      <div class="thesis-supervisor">
        {% if thesis.supervisors.size == 1 %}Supervisor: {{ thesis.supervisors[0] }}
        {% else %}Supervisors:
          {% for supervisor in thesis.supervisors %}{{ supervisor }}{% unless forloop.last %}{% if forloop.rindex == 2 %} and {% else %}, {% endif %}{% endunless %}{% endfor %}
        {% endif %}
      </div>
      {% endif %}
    </li>
    {% endfor %}
  </ul>
</section>
{% endfor %}
