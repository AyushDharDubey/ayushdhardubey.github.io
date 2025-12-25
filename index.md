---
layout: default
tags: home
---

## Hi there,<br/>I'm Ayush Dhar Dubey.

### I’m a developer with a particular interest in open-source work, particularly in the OpenStreetMap and Django ecosystems.

### I currently help build [3DMR](https://wiki.openstreetmap.org/wiki/3D_Model_Repository), with the aim of improving the quality of the 3D renderers available in OSM.

<br/>

I spend most of my time contributing to open-source projects or reading. A few things that keep me occupied:

- Good books. Two recent favourites: _शेखर: एक जीवनी_ (अज्ञेय) and _Extreme Ownership_ (Jocko Willink & Leif Babin).  
- OpenStreetMap and its surrounding projects  
- Distance running, mostly as an excuse to get outside  

<br/>

[**See my latest blog posts →**]({{ site.baseurl }}/blogs)

<ul>
  {% for post in site.posts limit:3 %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <span class="post-meta">{{ post.date }}</span>
    </li>
  {% endfor %}
</ul>
