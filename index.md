---
layout: default
---
# About
## About me

I'am not a professional, but love to create effects on the **Shadertoy** web site.

[Here](https://www.shadertoy.com/user/sylvain69780) a link to Shadertoy showing my published shaders.

And in [this post]({% post_url 2020-01-01-my-published-shaders %}) a commented list of it.

In [this post]({% post_url 2021-04-02-notes-about-some-shaders %}) a database of of the shaders I noted.

I also have another [Blog](https://sylvain69780.github.io/digital-culture/) to initiate child and olders to some computer culture.

# Posts 

{% for tag in site.tags %}
  <h2>{{ tag[0] }}</h2>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.date | date: "%Y-%m-%d" }} {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
