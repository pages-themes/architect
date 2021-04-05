---
layout: default
title: "Impress your friends by Live coding the manderbrot's Set fractal on Shadertoy"
tags: shadertoy
---

I know because I already coded it on my ATARI 520 ST, it's a very easy fractal to compute.

[The definition](https://en.wikipedia.org/wiki/Mandelbrot_set) is trivial, if you just have an idea of what complex numbers are (it's not so complex !)

You just need this little complex number multiplication function to compute Z*Z.

```
vec2 cmpxmul(in vec2 a, in vec2 b) {
	return vec2(a.x * b.x - a.y * b.y, a.y * b.x + a.x * b.y);
}
```

Iq made a short verion of it here :

{% for shader in site.data.shaders %}
{% if shader.id == "lllGWH" %}
![{{ shader.title }}](https://www.shadertoy.com/media/shaders/{{ shader.id }}.jpg)  
**[{{ shader.title }}](https://www.shadertoy.com/view/{{ shader.id }})** by **[{{ shader.author }}](https://www.shadertoy.com/user/{{ shader.author }})**

>{{ shader.comments }} 
{% endif %}
{% endfor %}

Please note that there is an infinite zoom possible on the Mandelbrot's set, the only limits are the precision of the float and the number of allowed iterations to compute the details of the set.
