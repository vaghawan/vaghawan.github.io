---
permalink: /
title: "Personal Github Page"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---
Please know that I'm naive and learning myself, so the mistakes may be prevailing on all bends..

Latest Posts
======
{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
