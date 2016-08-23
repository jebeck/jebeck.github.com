---
layout: default
title: home
---

<section class="home">
  {% include intro.html %}
  <h2 class="posts-title">recent blog posts</h2>
  <ul class="posts">
    {% for post in site.posts %}
      {% if forloop.index <= 3 %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y:" }}</span>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">
          {{ post.title }}
        </a>
      </li>
      {% endif %}
    {% endfor %}
  </ul>
</section>