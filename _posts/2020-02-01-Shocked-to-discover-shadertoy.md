---
layout: default
title:  "Shocked to 'Discover' Shadertoy"
tags : shadertoy
---

In March 2020, the COVID made me having more time to search about creative coding.

And in fact I discovered more than I expected !

| Shader | Comments | Preview |
| -------- | -------- | -------- |
| [IQ - Happy Jumping](https://www.shadertoy.com/view/3lsSzf) | Inigo impressive near 6 hour tutorial "LIVE Coding and Painting with Maths" | ![No Preview](https://www.shadertoy.com/media/shaders/3lsSzf.jpg) |

{% for shader in site.data.shaders reversed %}
  ![{{ shader.title }}](https://www.shadertoy.com/media/shaders/{{ shader.id }}.jpg)  
**[{{ shader.title }}](https://www.shadertoy.com/view/{{ shader.id }})** by **[{{ shader.author }}](https://www.shadertoy.com/user/{{ shader.author }})**

>{{ shader.comments }} 
{% endfor %}

* I (re)discovered the **demoscene** and their community very active on Shadertoy.
* I **discovered** with Shadertoy **the ray marching** algorithm that allows to build real time realistic 3D scenes "without any Maya or Blender or something", just your keyboard, some calculations on a paper sheet and knownlege of how to make a "for" loop. 
* My vision is that this site started from the very generous idea of **"Create and Share your best shaders with the world and find Inspiration"**. It's a place to watch small pieces of **GLSL** code generating awesome images. It's so rare today to find people driven only by their passion.

