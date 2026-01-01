---
layout: page
title: Library
permalink: /library/
---

Here are my latest posts:

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <span class="post-meta">{{ post.date }}</span>
    </li>
  {% endfor %}
</ul>
