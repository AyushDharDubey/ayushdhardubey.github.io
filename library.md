---
layout: page
title: Library
permalink: /library/
---

Selected books that I’ve read for enjoyment or learning.
To see things I haven’t yet read browse the [/anti-library]({{ site.baseurl }}/anti-library). All my (crappy) book reviews are at [/reviews]({{ site.baseurl }}/reviews).


<h1>Library</h1>
<section style="display: flex; justify-content: center; flex-wrap: wrap; gap: 40px;">
  {% for book in site.data.books %}
  <article style="flex: 1; max-width: 180px; padding-top: 5%;">
    <a href="{{ book.url | default: '#' }}" style="color: #222222">
        <div style="width: 180px"><img src="{{ book.cover }}" alt="{{ book.title }} cover" width="180" ></div>
        <div style="width: 180px">
            <h3>{{ book.title }}</h3>
            <p class="author">{{ book.author }}</p>
        </div>
    </a>
  </article>
  {% endfor %}
</section>