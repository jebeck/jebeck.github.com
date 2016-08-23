---
layout: default
title: about
---

<div class="home">
  {% include intro.html %}
  <section class="about">
    {% capture included %}{% include about_me.md %}{% endcapture %}
    {{ included | markdownify }}
  </section>
</div>