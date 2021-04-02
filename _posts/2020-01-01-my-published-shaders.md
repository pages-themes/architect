---
layout: default
title: "Why I felt the need to blog about Shadertoy"
tags: shadertoy
---
[Here](https://www.shadertoy.com/user/sylvain69780) a link to Shadertoy showing my published shaders.

Below my experiments, from most recent to olders.

{% for my_shaders in site.data.my_shaders reversed %}
  ![{{ my_shaders.title }}](https://www.shadertoy.com/media/shaders/{{ my_shaders.id }}.jpg)  
**[{{ my_shaders.title }}](https://www.shadertoy.com/view/{{ my_shaders.id }})** by **[{{ my_shaders.author }}](https://www.shadertoy.com/user/{{ my_shaders.author }})**

>{{ my_shaders.comments }} 
{% endfor %}
