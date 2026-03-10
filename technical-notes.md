---
layout: page
title: Technical Notes
lead: Deep dives into one technical idea at a time, aggregated across projects and ordered by date.
permalink: /technical-notes/
---
{% assign technical_notes = site.pages | where: "kind", "note" | sort: "date" | reverse %}

{% if technical_notes.size > 0 %}
{% for item in technical_notes %}
<article class="list-panel">
  <h3><a href="{{ item.url | relative_url }}">{{ item.title }}</a></h3>
  <p class="card-meta">{{ item.project_title }}{% if item.date %} · {{ item.date | date: "%d %b %Y" }}{% endif %}</p>
  {% if item.summary %}
  <p>{{ item.summary }}</p>
  {% endif %}
</article>
{% endfor %}
{% else %}
<p>No technical notes published yet.</p>
{% endif %}
