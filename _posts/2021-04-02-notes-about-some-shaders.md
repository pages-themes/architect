---
layout: default
title: Usefull notes about some Shaders
tags: shadertoy
---

{% assign shaders_by_category = site.data.shaders | group_by:"category" %}

{% for category in shaders_by_category %}

{{category.name}}

{% for shader in category.items %}
![{{ shader.title }}](https://www.shadertoy.com/media/shaders/{{ shader.id }}.jpg)  
**[{{ shader.title }}](https://www.shadertoy.com/view/{{ shader.id }})** by **[{{ shader.author }}](https://www.shadertoy.com/user/{{ shader.author }})**

>{{ shader.comments }} 
{% endfor %}
{% endfor %}

