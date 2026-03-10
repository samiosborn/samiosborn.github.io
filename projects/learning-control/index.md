---
layout: page
title: Learning & Control
lead: Reinforcement learning and controller-learning systems.
permalink: /projects/learning-control/
---
{% assign items = site.pages | where: "kind", "project" | where: "category", "learning-control" | sort: "order" %}

<div class="card-grid">
  {% for item in items %}
    <article class="card">
      <h3><a href="{{ item.url | relative_url }}">{{ item.project_title }}</a></h3>
      {% if item.summary %}
        <p>{{ item.summary }}</p>
      {% endif %}
    </article>
  {% endfor %}
</div>
