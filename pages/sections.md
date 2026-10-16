---
layout: page
title: Sections
permalink: /sections/
description: Section meeting times, guest speakers, the attendance policy, and how to prepare for discussion.
---

<dl class="logistics">
  <dt>Time</dt><dd>Thursday or Friday, 2:30–3:20pm (optional)</dd>
  <dt>Location</dt><dd>Room 14, basement of the Crown Building, Stanford Law School</dd>
  <dt>Section leaders</dt><dd>Dominic Zappia, Yifei Cheng, Bruria Friedman-Feldman (law), Yasi Khan, Tia Vasudeva</dd>
</dl>

In addition to the lectures on Mondays and Wednesdays, we will also hold optional
sections on Thursday or Friday. These sections will allow you to discuss and engage
with the course material in greater depth.

## Section slides

<!-- Built from the `section: true` rows of the _modules calendar, the same rows
     that feed /schedule/, so a deck added there (`slides:` on the row) shows up
     here too. Each section's Thursday is the day after the lecture before it. -->

{% assign units = site.modules | where: "year", site.current_year | sort: "order" %}
<dl class="lecture-index">
{% for unit in units %}{% for row in unit.rows %}
  {% if row.lecture %}{% assign prev = site['2026'] | where: 'lecture', row.lecture | first %}{% endif %}
  {% if row.section %}
  {% assign thu = prev.date | date: '%s' | plus: 86400 %}
  {% assign fri = thu | plus: 86400 %}
  <dd class="lecture-index-item">
    <span class="lecture-index-num">{{ row.week }}</span>
    <span>{{ thu | date: '%b %-d' }}/{{ fri | date: '%-d' }}</span>
    <span class="cal-slides">{% if row.slides %}<a href="{{ row.slides | relative_url }}">[slides]</a>{% else %}<span class="cal-slides-tbd">[slides]</span>{% endif %}</span>
  </dd>
  {% endif %}
{% endfor %}{% endfor %}
</dl>

## Distinguished guests and supplementary workshops

We will also be hosting several guest speakers outside of class throughout the
term, and we encourage you to attend those sessions.

On Thursdays from 12:40 to 2:00pm in Room 270 in SLS Crown (over the breezeway), the Law
School's AI Initiative holds its weekly speaker series, featuring leading figures
in the AI ecosystem. Lunch is provided, so please RSVP every time you would like
to attend, and everyone should register to receive emails from the Initiative.
Sign up for emails and RSVP for events at
[law.stanford.edu/ai-initiative/events-ai](https://law.stanford.edu/ai-initiative/events-ai/)
(email registration is at the bottom of the page).
