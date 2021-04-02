---
layout: default
---
# About
## My Shadertoy published Shaders

I'am not a professional, but love to create effects on the **Shadertoy** web site.

[Here](https://www.shadertoy.com/user/sylvain69780) a link to my experiments.

{% for my_shaders in site.data.my_shaders %}
  [{{ my_shaders.title }}](https://www.shadertoy.com/view/{{ my_shaders.id }})
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
