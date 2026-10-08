---
layout: default
title: PhD Theses | AMASES
description: >-
  Discover PhD theses that have been written by scholars related to AMASES.
---

<h1>PhD Theses</h1>

<p class="intro">
This is a list of {{ site.data.theses | size }} PhD theses in fields related to <a href="https://www.amases.org">AMASES</a> (Association for Mathematics
Applied to Economic and Social Sciences). It collects entries submitted by authors or supervisors, as well as all works archived by the <a href="https://tesidottorato.depositolegale.it">Biblioteca Centrale di Firenze</a> in association with the 2000 code for "Mathematical Methods for Economics, Finance, and Insurance". Requests for additions or correction are welcome. [Contact us](mailto:alessandra.cretarola@unich.it).

AMASES is aware that each language has different conventions: therefore, titles in English are capitalized while titles in Italian or French are lowercased.   
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
