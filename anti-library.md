---
layout: page
title: Anti-Library
permalink: /anti-library/
---

Books I haven’t read, but like the idea of having read, and plan to read in the future.


<h1>Anti-Library</h1>
<section style="display: flex; justify-content: center; flex-wrap: wrap; gap: 40px;">
  {% for book in site.data.books %}
  {% if not book.read %}
  <article style="flex: 1; max-width: 180px; padding-top: 5%;">
    <a href="{{ book.url | default: '#' }}" style="color: #222222">
        <div style="width: 180px"><img src="{{ book.cover }}" alt="{{ book.title }} cover" width="180" ></div>
        <div style="width: 180px">
            <h3>{{ book.title }}</h3>
            <p class="author">{{ book.author }}</p>
        </div>
    </a>
  </article>
  {% endif %}
  {% endfor %}
</section>