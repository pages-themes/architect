---
layout: default
title: "Dihedral angle and the scorpius spider slider puzzle"
tags: shadertoy
---

# What is this ?

I have the **chance** to own a "scorpius slider spider puzzle", a piece of **wood art** bought 30 years ago.

![preview](https://static.blog4ever.com/2008/06/213622/artfichier_213622_8769121_202010012502419.png)

I learnt reading [this article of Philippe Cichon](https://www.lairdubois.fr/creations/14279-le-scorpius.html) that it's a rare puzzle, very few makers exists.

The shape is very cool and I tried to reproduce it on Shadertoy. For this I needed to understand the geometry in place here.

This video of Philippe Cichon shows how to mount and unmout it (in French)
[Le Scorpius on Youtube](https://www.youtube.com/watch?time_continue=13&v=2orJ6rTSx2s&feature=emb_logo)

# The Dihedrial angle problem

What fascinated me is the rotation angle needed to bend each little piece when mounting the puzzle.

Refering to the article on "L'air du bois", this bend angle is 70 degres, but why this value ?  
All pieces have a triangular section, with angles 30, 60 and 90 degres, this is an half equilateral triangle with sides 1,2,sqrt(3), but when assembled, all pieces are connected with a symetry of 90 degres around a central point.

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
    // Bend angle of approx 70,52877937 degres
    // This is the first key value to build the puzzle
    float r = acos(1./3.);
```

>I found interesting that the Wikipedia page speaking about the [Rhombic dodecahedron](https://en.wikipedia.org/wiki/Rhombic_dodecahedron) mention that **arccos(1/3)** is the acute angles on each face.

The French version says that it's value is **2*arctan(1/√2)** and it appears that this is the same value. I would be happy to have the explanation of this strange equivalence.

```
2*arctan(1/√2)-arccos(1/3) = 0
```

[I verified with Wolfram](https://www.wolframalpha.com/input/?i=2*arctan%281%2F%E2%88%9A2%29-arccos%281%2F3%29)

# Position of the contact surfaces and pin point on each face

One can find on [this schema](https://sylvain69780.github.io/assets/images/scorpius_puzzle.svg) the calculations using painfull but basic trigonomerty formulas.

![preview](https://sylvain69780.github.io/assets/images/scorpius_puzzle.svg)

# Is it possible to use polar domain repetition ?

Domain repetition enables to compute a shape only once by defining repetition domains, like a grid for example.  
The polar repetition is based on non-overlapping domains, and the bending of the pieces makes this [impossible](https://www.shadertoy.com/view/slfGDf). But we can use a simple dicotomy to identify the domain by testing the dihedral plans.  
This is in relation with [Wythoff polyhedrons](https://www.shadertoy.com/results?query=tag%3Dwythoff) on Shadertoy.  
We also need to take these plans into account in the ray marching. This is quite complicated but needs to be tried but time is missing.

