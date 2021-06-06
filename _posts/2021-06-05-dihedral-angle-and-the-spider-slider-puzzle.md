---
layout: default
title: "Dihedral angle and the scorpius spider slider puzzle"
tags: shadertoy
---

# What is this ?

I had the **chance** to own a "scorpius slider spider puzzle", a piece of **wood art** that is still kept by my parents.

![preview](https://static.blog4ever.com/2008/06/213622/artfichier_213622_8769121_202010012502419.png)

I learnt reading [this article of Philippe Cichon](https://www.lairdubois.fr/creations/14279-le-scorpius.html) that it's a rare puzzle, very few makers exists.

The shape is very cool and I tried to reproduce it on Shadertoy. For this I needed to understand the geometry in place here.

This video of Philippe Cichon shows how to mount and unmout it (in French)
[Le Scorpius on Youtube](https://www.youtube.com/watch?time_continue=13&v=2orJ6rTSx2s&feature=emb_logo)

# The Dihedrial angle problem

What fascinated me is the rotation angle needed to bend each little piece when mounting the puzzle.

Refering to the article on "L'air du bois", this bend angle is 70 degres, but why this value ?  
All pieces have a triangular section, with angles 30, 60 and 90 degres, this is an half equilateral triangle with side 1,2,sqrt(3), but when assembled, all pieces are connected with a symetry of 90 degres around a central point.

I suspected that 70 degres was not an exact value, and wanted to compute it by myself using some basic geometry. It was not so easy.

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/Nlf3W2?gui=true&t=10&paused=true&muted=false" allowfullscreen></iframe>

# Calculation of the bend angle

When assembled, the Dihedral angle of the planes formed by the **connected faces** of one piece and the next one should be 90 degres, in order to get this **4 times** rotation symetry.

The [Dihedral angle](https://mathworld.wolfram.com/DihedralAngle.html) is **cos(angle) = dot(n1,n2)**. n1 and n2 are the normals of the planes.
- we want the angle between the faces to be 90 degres
- as cos(90 degres)=0 we need to solve dot(n1,n2) = 0.

We can compute that  
```
n1 = vec3(-sqrt(3),1/2,0)  
n2 = vec3(-cos(rotation)* sqrt(3)/2,-1/2,-sin(rotation)*sqrt(3)/2)
```
the dot product simplifies to cos(rotation)=1/3, meaning 
```
rotation = acos(1/3) = 70,5287294 degres
```

Below a 2D geomery I tried on [Desmos](https://www.desmos.com/geometry/g1cdjpyrzq) showing from the top the pieces connected before the rotation.
![preview](/assets/images/dihedral_desmos.png)

Next challenge is to find the exact location for the pin points between 2 pieces. To be continued.
