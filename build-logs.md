---
layout: page
title: Build Logs
lead: Dated engineering progress updates across all projects, newest first.
permalink: /build-logs/
---
{% assign build_logs = site.pages | where: "kind", "build-log" | sort: "date" | reverse %}

{% if build_logs.size > 0 %}
{% for item in build_logs %}
<article class="list-panel">
  <h3><a href="{{ item.url | relative_url }}">{{ item.title }}</a></h3>
  <p class="card-meta">{{ item.project_title }}{% if item.date %} · {{ item.date | date: "%d %b %Y" }}{% endif %}</p>
  {% if item.summary %}
  <p>{{ item.summary }}</p>
  {% endif %}
</article>
{% endfor %}
{% else %}
<p>No build logs published yet.</p>
{% endif %}
