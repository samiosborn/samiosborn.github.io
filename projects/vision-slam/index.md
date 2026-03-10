---
layout: page
title: Vision & SLAM
lead: Geometric perception and mapping projects.
permalink: /projects/vision-slam/
---
{% assign items = site.pages | where: "kind", "project" | where: "category", "vision-slam" | sort: "order" %}

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
