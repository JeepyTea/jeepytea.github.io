---
layout: default
title: Home
---

# Welcome to My Blog

This is a beautiful GitHub Pages blog where I share my thoughts, projects, and ideas.

## Recent Posts

{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url | relative_url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

## About Me

I'm passionate about technology, design, and creating amazing things. This blog is a space where I document my journey and share what I learn along the way.

[Read more about me](/about)
