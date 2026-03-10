---
layout: page
title: Robotics
lead: Embodied systems, control loops, and hardware-software integration.
permalink: /projects/robotics/
---
{% assign items = site.pages | where: "kind", "project" | where: "category", "robotics" | sort: "order" %}

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
