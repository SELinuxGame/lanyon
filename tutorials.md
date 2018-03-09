---
layout: page
title: Tutorials
---

All of the tutorials below are designed to teach SELinux commands used in the
scenarios. These are self-guided and provide concrete examples. They build on
each other, so going top to bottom is recommended.

Each of these can be tested with the `tutorials` box. More instructions on
loading this box are on the tutorial pages.

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
{% assign sorted_tutorials = site.tutorials | sort: 'number' %}
{% for tutorial in sorted_tutorials %}
    <tr>
      <td><a href="{{ layout.rel_path }}{{ tutorial.url }}">{{ tutorial.title }}</a></td>
      <td>{{ tutorial.description }}</td>
    </tr>
{% endfor %}
  </tbody>
</table>
