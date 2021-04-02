---
layout: default
---
# About
## My Shadertoy published Shaders

I'am not a professional, but love to create effects on the **Shadertoy** web site.

[Here](https://www.shadertoy.com/user/sylvain69780) a link to Shadertoy showing my published shaders.

And in [this post]({% post_url 2020-01-01-my-published-shaders %}) a commented list of it.

# Posts 

{% for tag in site.tags %}
  <h2>{{ tag[0] }}</h2>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.date | date: "%Y-%m-%d" }} {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
