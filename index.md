---
layout: default
title: home
---

### (&#x02c8;d͡ʒæ·nə bɛk)

<div class="home">
  <p id="me-short">
    software engineer. Pw(t1)D. car-free bike &amp; public transportation commuter. world traveler. coffee <del>connoisseur</del> snob. hobbyist dancer.
  </p>
  <h2 class="posts-title" id="maincontent">recent blog posts</h2>
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
</div>