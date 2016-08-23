---
layout: default
title: archive
---

<section class="archive">
  <h2 class="posts-title">all blog posts</h2>
  <ul class="posts">
    {% for post in site.posts %}
    <li>
      <span class="post-meta">{{ post.date | date: "%b %-d, %Y:" }}</span>
      <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">
        {{ post.title }}
      </a>
    </li>
    {% endfor %}
  </ul>
</section>