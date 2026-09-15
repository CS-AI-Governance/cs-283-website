---
layout: page
title: Lectures
permalink: /lectures/
description: All CS283 lectures, grouped by unit, with links to each session's readings.
---

Each lecture page carries its summary and the full required and supplementary
reading list. Reading lists are subject to change and may be updated up until two
weeks before the lecture.

<!-- Rendered from the per-year _2026 collection, grouped by the `unit` field:
     the thematic units of the course map, in date order. -->

{% assign lectures = site['2026'] | sort: 'date' %}
{% assign units = lectures | group_by: 'unit' %}

<dl class="lecture-index">
{% for unit in units %}
  {% assign first = unit.items | first %}
  <dt class="lecture-index-week">{{ first.unit_title }}</dt>
  {% for lecture in unit.items %}
  <dd class="lecture-index-item">
    <span class="lecture-index-num">{{ lecture.lecture }}</span>
    {% if lecture.ready %}<a href="{{ lecture.url | relative_url }}">{{ lecture.title }}</a>{% else %}{{ lecture.title }}{% endif %}
    <span class="lecture-index-date">{{ lecture.date | date: '%a, %b %-d' }}</span>
  </dd>
  {% endfor %}
{% endfor %}
</dl>
