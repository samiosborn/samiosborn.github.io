---
layout: page
title: Research Reflections
lead: Essays and strategic reflections across projects and broader technical themes, ordered by date.
permalink: /research-reflections/
---
{% assign reflections = site.pages | where: "kind", "reflection" | sort: "date" | reverse %}

{% if reflections.size > 0 %}
{% for item in reflections %}
<article class="list-panel">
  <h3><a href="{{ item.url | relative_url }}">{{ item.title }}</a></h3>
  <p class="card-meta">{% if item.project_title %}{{ item.project_title }} · {% endif %}{% if item.date %}{{ item.date | date: "%d %b %Y" }}{% endif %}</p>
  {% if item.summary %}
  <p>{{ item.summary }}</p>
  {% endif %}
</article>
{% endfor %}
{% else %}
<p>No research reflections published yet.</p>
{% endif %}
