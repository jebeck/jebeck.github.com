---
layout: default
title: projects
---

## side projects

#### (a selection, in various degrees of progress)

{% for project in site.data.projects %}
<section class="project">
  <h3 class="project-name">{{ project.emoji }} {{ project.name }}</h3>
  <div class="links">
    {% if project.link %}
      <div class="link">
        <span>&lt;</span><a href='{{ project.link }}'>view live</a><span>&gt;</span>
      </div>
    {% endif %}
    {% if project.github %}
      <div class="link">
        <span>[</span><a href='{{ project.github }}'>code on GitHub</a><span>]</span>
      </div>
    {% endif %}
    {% if project.npm %}
      <div class="link">
        <span>{</span><a href='{{ project.npm }}'>package on npm</a><span>}</span>
      </div>
    {% endif %}
    {% if project.docs %}
      <div class="link">
        <span>(</span><a href='{{ project.docs }}'>docs</a><span>)</span>
      </div>
    {% endif %}
  </div>
  <div class="technologies">
    {% for tech in project.technologies %}
    <span>{{ tech }}</span>
    {% endfor %}
  </div>
  <p>{{ project.description | markdownify }}</p>
  {% for sub in project.associated %}
    <h4 class="associated">{{ sub.emoji }} {{ sub.name }}</h4>
    <div class="links">
      {% if sub.link %}
        <div class="link">
          <span>&lt;</span><a href='{{ sub.link }}'>view live</a><span>&gt;</span>
        </div>
      {% endif %}
      {% if sub.github %}
        <div class="link">
          <span>[</span><a href='{{ sub.github }}'>code on GitHub</a><span>]</span>
        </div>
      {% endif %}
      {% if sub.npm %}
        <div class="link">
          <span>{</span><a href='{{ sub.npm }}'>package on npm</a><span>}</span>
        </div>
      {% endif %}
    </div>
    <p>{{ sub.description }}</p>
  {% endfor %}
</section>
{% endfor %}