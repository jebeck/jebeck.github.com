---
layout: default
title: speaking
---

<section class="speaking">
  {% capture included %}{% include speaking.md %}{% endcapture %}
  {{ included | markdownify }}
</section>
