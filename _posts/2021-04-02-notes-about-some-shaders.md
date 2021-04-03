---
layout: default
title: Usefull notes about some Shaders
tags: shadertoy
---

{% assign shaders_by_category = data.shaders | group_by:"category" %}

{% for category in shaders_by_category %}
  <dt>{{category.name}}</dt>
  {% for shader in category.items %}
  <dd><a href="{{post.url}}">{{post.title}}</a></dd>
  {% endfor %}
{% endfor %}

