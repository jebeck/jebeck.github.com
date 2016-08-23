---
layout: default
title: résumé
---

<section class="resume">
  {% capture included %}{% include resume.md %}{% endcapture %}
  {{ included | markdownify }}
</section>