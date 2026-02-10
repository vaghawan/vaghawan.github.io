---
permalink: /
title: "Personal Github Page"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Latest Posts
======
{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
