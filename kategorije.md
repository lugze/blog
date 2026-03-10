---
layout: page
title: Kategorije
permalink: /kategorije/
---

Vidi također: [📄 Dokumentacija]({{ "/dokumentacija/" | relative_url }}) · [📋 Zapisnici]({{ "/zapisnici/" | relative_url }})

<div class="category-section">
  <h3>🐧 Linux</h3>
  <ul>
    {% for post in site.categories.linux %}
      {% if post.url %}
        <li><a href="{{ post.url | relative_url }}">🔹 {{ post.title }}</a></li>
      {% endif %}
    {% endfor %}
  </ul>
</div>

<div class="category-section">
  <h3>💎 Ruby</h3>
  <ul>
    {% for post in site.categories.ruby %}
      {% if post.url %}
        <li><a href="{{ post.url | relative_url }}">🔹 {{ post.title }}</a></li>
      {% endif %}
    {% endfor %}
  </ul>
</div>

<div class="category-section">
  <h3>📝 Blog</h3>
  <ul>
    {% for post in site.categories.blog %}
      {% if post.url %}
        <li><a href="{{ post.url | relative_url }}">🔹 {{ post.title }}</a></li>
      {% endif %}
    {% endfor %}
  </ul>
</div>

<div class="category-section">
  <h3>👥 LugZe</h3>
  <ul>
    {% for post in site.categories.lugze %}
      {% if post.url %}
        <li><a href="{{ post.url | relative_url }}">🔹 {{ post.title }}</a></li>
      {% endif %}
    {% endfor %}
  </ul>
</div>
