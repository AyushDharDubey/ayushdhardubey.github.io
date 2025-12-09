---
layout: page
title: Library
permalink: /library/
---

Selected books that I’ve read for enjoyment or learning.
To see things I haven’t yet read browse the [/anti-library]({{ site.baseurl }}/anti-library). All my (crappy) book reviews are at [/reviews]({{ site.baseurl }}/reviews).


<h1>Library</h1>
<div class="book-grid">
  {% for book in site.data.books %}
  <article class="book-card">
    <a href="{{ book.url | default: '#' }}">
        <img src="{{ book.cover }}" alt="{{ book.title }} cover" />
    </a>
    <h3>{{ book.title }}</h3>
    <p class="author">{{ book.author }}</p>
  </article>
  {% endfor %}
</div>
