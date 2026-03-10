---
layout: page
title: Zapisnici
permalink: /zapisnici/
---

Zapisnici sa sastanaka Udruzenja Linux Korisnika Zenice.

<ul>
  {% assign zapisnici = site.posts | where_exp: "post", "post.title contains 'Zapisnik'" %}
  {% for post in zapisnici %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <small>({{ post.date | date: "%d.%m.%Y." }})</small>
    </li>
  {% endfor %}
</ul>
