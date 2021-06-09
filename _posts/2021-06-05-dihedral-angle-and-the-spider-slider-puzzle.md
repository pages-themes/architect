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

Below [a 2D geomery I tried on Desmos](https://www.desmos.com/geometry/g1cdjpyrzq) showing from the top the pieces connected before the rotation.
![preview](/assets/images/dihedral_desmos.png)

Next challenge is to find the exact location for the pin points between 2 pieces. To be continued.

# Elevation of upper corner point

In our figure, we are putting edge to edge 2 identical pieces and rotated the first one of r=acos(1/3).
[we are searching point P in this Desmos schema](https://www.desmos.com/geometry/s4evom660u)

The intersection point of the two left edges is by construct ```vec2(0.0,0.0)```
We are now searching for the Y coordinate ```vec2(0.0,d0)``` of the intersection point of the right edge of the second rotated piece with the left border of the first piece. (y axis).  

This is important because it gives the top end of the piece, and will allow to position all other geometry like the pin points.

>Again we compute an half equilateral triangle with sides 1,2,sqrt(3), and will multiply by 15 to have the final proportions of the Puzzle.

```
s = 15.0
r = acos(1.0/3.0)
c = 0.9
```

We can see that the surface of superposition of the 2 faces forms a parallelogram.
The triangle OHP is rectangle, with OH=2*s*c and angle HPO = arccos(1/3).
OP length is the value **l** that we are looking at.
Sinus is [opposite side on Hypotenuse](https://www.mathsisfun.com/sine-cosine-tangent.html) so
sin(arccos(1/3)) = OH / OP

```
l = 2*s*c/sin(r)
```

```
    float c = 0.9; // pct of cut of the sharper edge.
    // elevation to reach the edge 
    // this is the second value usefull to build the puzzle.
    // For building the wood puzzle l = 15 * 1,909188309 = 28,63782464 mm 
    float l = 2.0*c/sin(r);
```

# Location on each face of the pin points

[Desmos Geometry of the plan connecting the pieces](https://www.desmos.com/geometry/eqby2qihrk?lang=fr)

We want the pin points to be on the middle line of each respective faces.

We localize the pin point on the little face, it's the intersection point between middle lines of each face, when the second face is bended to 70 degres.  
Using the slope of the middle line of the second face, we can compute that it crosses the middle line of the first face at ```vec2(.5,0.5*el-.5/tan(r))```

```
    // Location of the pin point
    // This is the 3rd value usefull to build the puzzle
    // For building the wood puzzle d1 = 15 * 0,777817459 = 11,66726189 mm 
    // The difference of elevation with the top of the piece is 16,97056275 mm
    float d1 = 0.5*l-.5/tan(r);
    vec2 p1 = vec2(.5,d1);    
```

Now, we have to find the location of the matching Hole on the larger face.

searching y for
vec2 p2 = vec2(l*0.5,y) rotated of 70 degres arrives on p1.

It appears that y is the distance of p1 to the line crossing the second face.
y = dot(p1,n)
n = vec2(-sin(r),cos(r))
y = dot(p1,vec2(-sin(r),cos(r)

```
    // Location of the hole of the pin point on the larger face
    // This is the 4th value usefull to build the puzzle
    // For building the wood puzzle d2 = 15 * -0,212132034 = -3,181980515 mm 
    float d2 = (l-1.0/tan(r))/6.0-.5*sin(r);
    vec2 p2 = vec2(c,d2); 
```

[Simplified on Desmos](https://www.desmos.com/geometry/xe3jsvrvck)

# Others measures

To be continued

# Is it possible to use polar domain repetition ?

Domain repetition enables to compute a shape only once by defining repetition domains, like a grid for example.  
The polar repetition is based on non-overlapping domains, and the bending of the pieces makes this [impossible](https://www.shadertoy.com/view/slfGDf). But we can use a simple dicotomy to identify the domain by testing the dihedral plans.  
This is in relation with [Wythoff polyhedrons](https://www.shadertoy.com/results?query=tag%3Dwythoff) on Shadertoy.  
We also need to take these plans into account in the ray marching. This is quite complicated but needs to be tried.
