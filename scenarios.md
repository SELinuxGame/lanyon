---
layout: page
title: Scenarios
---

The Scenarios are listed below grouped by difficulty.

## Easy

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
{% for scenario in site.scenarios %}
  {% if scenario.difficulty == 'easy' %}
    <tr>
      <td><a href="{{ layout.rel_path }}{{ scenario.url }}index.html">{{ scenario.title }}</a></td>
      <td>{{ scenario.description }}</td>
    </tr>
  {% endif %}
{% endfor %}
  </tbody>
</table>

## Medium

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
{% for scenario in site.scenarios %}
  {% if scenario.difficulty == 'medium' %}
    <tr>
      <td><a href="{{ layout.rel_path }}{{ scenario.url }}">{{ scenario.title }}</a></td>
      <td>{{ scenario.description }}</td>
    </tr>
  {% endif %}
{% endfor %}
  </tbody>
</table>

## Hard

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
{% for scenario in site.scenarios %}
  {% if scenario.difficulty == 'hard' %}
    <tr>
      <td><a href="{{ layout.rel_path }}{{ scenario.url }}">{{ scenario.title }}</a></td>
      <td>{{ scenario.description }}</td>
    </tr>
  {% endif %}
{% endfor %}
  </tbody>
</table>
