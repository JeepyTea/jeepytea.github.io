---
layout: default
title: Home
---

{% for post in site.posts limit:5 %}
<article class="post-preview">
  <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
  
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
  
  <div class="post-content">
    {{ post.content }}
  </div>
</article>

<hr>
{% endfor %}

<div class="about-section">
  <h2>About Me</h2>
  <p>I'm passionate about technology, AI, and creating amazing things. This blog is a space where I document my journey and share what I learn along the way.</p>
  <p><a href="/about" class="about-link">Read more about me</a></p>
</div>
