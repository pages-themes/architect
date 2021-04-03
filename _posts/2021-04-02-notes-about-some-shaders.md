---
layout: default
title: Usefull notes about some Shaders
tags: shadertoy
---

I made a database of shaders I reviewed, but will prefer to make playlists in shadertoy instead.

* [Blog - Discovered Shadertoy](https://www.shadertoy.com/playlist/MXtXWl)
>Inigo's impressive near 6 hours tutorial "LIVE Coding and Painting with Maths" available on Youtube
* [Blog - Video Jockey](https://www.shadertoy.com/playlist/XXyXzR)
>I noticed great creations that would be great in a party !

{% assign shaders_by_category = site.data.shaders | group_by:"category" %}

{% for category in shaders_by_category %}

# {{category.name}}

{% for shader in category.items %}
![{{ shader.title }}](https://www.shadertoy.com/media/shaders/{{ shader.id }}.jpg)  
**[{{ shader.title }}](https://www.shadertoy.com/view/{{ shader.id }})** by **[{{ shader.author }}](https://www.shadertoy.com/user/{{ shader.author }})**

>{{ shader.comments }} 
{% endfor %}
{% endfor %}

