---
title: "Dreams are the seedlings of reality"
layout: splash
permalink: /
excerpt: "Napoleon Hill 'Think and Grow Rich'"
header:
  overlay_color: "#6C757D"
---

<div class="grid__wrapper">
  {% for post in site.posts limit:8 %}
    {% include archive-single.html type="grid" %}
  {% endfor %}
</div>
