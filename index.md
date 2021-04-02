---
layout: default
---
# About
## My Shadertoy published Shaders

I'am not a professional, but love to create effects on the **Shadertoy** web site.

[Here](https://www.shadertoy.com/user/sylvain69780) a link to Shadertoy showing my published shaders.

Below my experiments, by order of creation time.

{% for my_shaders in site.data.my_shaders %}
  ![{{ my_shaders.title }}](https://www.shadertoy.com/media/shaders/{{ my_shaders.id }}.jpg)  
**[{{ my_shaders.title }}](https://www.shadertoy.com/view/{{ my_shaders.id }})** by **[{{ my_shaders.author }}](https://www.shadertoy.com/user/{{ my_shaders.author }})**

>{{ my_shaders.comments }} 
{% endfor %}

# Posts 

{% for tag in site.tags %}
  <h2>{{ tag[0] }}</h2>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.date | date: "%Y-%m-%d" }} {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
