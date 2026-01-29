---
layout: page
title: Blog
permalink: /blog/
---

# Blog Posts

{% for post in site.posts %}
  <article>
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p>{{ post.date | date: "%b %-d, %Y" }}</p>
    <p>{{ post.excerpt }}</p>
  </article>
{% endfor %}
