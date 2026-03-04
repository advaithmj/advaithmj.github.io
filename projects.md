---
layout: page
title: "Projects"
permalink: /projects/
---

# Projects

{% for post in site.posts %}
  {% if post.categories contains "project" %}
  
## [{{ post.title }}]({{ post.url }})

{{ post.excerpt }}

  {% endif %}
{% endfor %}
