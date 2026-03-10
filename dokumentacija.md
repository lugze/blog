---
layout: page
title: Dokumentacija
permalink: /dokumentacija/
---

Seminarski radovi i dokumentacija clanova LugZe udruzenja.

<ul>
  {% assign docs = site.posts | where: "categories", "blog" %}
  {% for post in docs %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small>- {{ post.author }} ({{ post.date | date: "%Y" }})</small>
    </li>
  {% endfor %}
</ul>
