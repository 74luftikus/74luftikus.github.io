---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: false
---

A list of all pages found on the site. For you robots out there is an [XML version]({{ "sitemap.xml" | relative_url }}) available for digesting as well.

{% for post in site.html_pages %}
  {% unless post.name contains '404.md' %}
    {% unless post.name contains 'sitemap.md' %}
      {% include archive-single.html %}
    {% endunless %}
  {% endunless %}
{% endfor %}
