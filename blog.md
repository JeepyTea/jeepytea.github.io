---
layout: default
title: Blog
---

# Blog

{% for post in site.posts %}
## [{{ post.title }}]({{ post.url | relative_url }})

<div class="post-meta">
  {{ post.date | date: "%B %d, %Y" }}
  {% if post.categories.size > 0 %}
  • 
  <span class="post-categories">
    {% for category in post.categories %}
    <a href="{{ '/categories/' | append: category | relative_url }}">{{ category }}</a>
    {% unless forloop.last %}, {% endunless %}
    {% endfor %}
  </span>
  {% endif %}
</div>

{{ post.excerpt }}

[Read more]({{ post.url | relative_url }})

<hr>
{% endfor %}
