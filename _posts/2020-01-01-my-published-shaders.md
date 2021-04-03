---
layout: default
title: "My Published Shaders on Shadertoy"
tags: shadertoy
---
[Here](https://www.shadertoy.com/user/sylvain69780) a link to Shadertoy showing my published shaders.

Below my experiments, from most recent to olders.

I don't publish all my creations and experiments, I only set a shader public when I think it's presentable and can be inspiring, I think this is what everyone is doing, this avoids to have too much public shaders to browse on Shadertoy. 

In general, I also try to gives instructions to have different fun results by a simple modification of a line of code. **This is a toy** ! 

Many times, friends ask me **how many time** it took to me to make these shaders.
I can tell between 10 to 20 hours of cumulated work in general to get a presentable result for the community and publish it. 

First have the idea and want to share it, work on the message associated to your creation, and good animation, limited artifacts, colors etc. 

As IQ repeat in these videos, **you just need to detect ugly things**, and this needs a lot of time for a newbie, but it's realy pleasant. And the more you learn, the more you are able to see ugly things to fix.

{% for my_shaders in site.data.my_shaders reversed %}
  ![{{ my_shaders.title }}](https://www.shadertoy.com/media/shaders/{{ my_shaders.id }}.jpg)  
**[{{ my_shaders.title }}](https://www.shadertoy.com/view/{{ my_shaders.id }})** by **[{{ my_shaders.author }}](https://www.shadertoy.com/user/{{ my_shaders.author }})**

>{{ my_shaders.comments }} 
{% endfor %}
