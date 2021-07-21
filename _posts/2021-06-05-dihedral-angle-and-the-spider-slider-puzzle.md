---
layout: default
title: "Dihedral angle and the scorpius spider slider puzzle"
tags: shadertoy
---

# Dihedral angle and the scorpius spider slider puzzle
## What is this ?

When I was a child, I had the chance to own a "scorpius slider spider puzzle", a piece of wood art bought 30 years ago.

![preview](https://static.blog4ever.com/2008/06/213622/artfichier_213622_8769121_202010012502419.png)

I learnt reading [Philippe Cichon's blog](https://puzzles-et-casse-tete.blog4ever.com/le-scorpius-1) that it's a rare puzzle, very few makers exists.

The shape is very cool and I tried to reproduce it on Shadertoy. For this I needed to understand the geometry in place here, with only my elementary knowledge. 

This video of Philippe Cichon shows how to mount and unmout it (in French)
[Le Scorpius on Youtube](https://www.youtube.com/watch?time_continue=13&v=2orJ6rTSx2s&feature=emb_logo)

## Calculation of the angle to bend the pieces : The Dihedrial angle

The rotation angle needed to bend each little piece when mounting the puzzle is quite annoying.

Refering to the article on [Philippe Cichon's blog (French)](https://puzzles-et-casse-tete.blog4ever.com/le-scorpius-1), this bend angle is 70 degres, but why this value ?  
All pieces have a triangular section, with angles 30, 60 and 90 degres, this is an half equilateral triangle with sides 1,2,sqrt(3), but when assembled, all 4 pieces are connected with a polar symetry of 90 degres around a central point.

I suspected that 70 degres was not an exact value, and wanted to compute it by myself using some basic geometry. Below my try for an explanation.

![faces numbers](https://static.blog4ever.com/2008/06/213622/artfichier_213622_8769120_202010011725351.png)
Philippe's picture with the numbering of the faces, convention I kept here.

A [dihedral angle](https://mathworld.wolfram.com/DihedralAngle.html) is the angle between two intersecting planes

![preview](https://sylvain69780.github.io/assets/images/scorpius_puzzle_angle.svg)

When assembled, the Dihedral angle of the planes of one pieces with the next one should be 90 degres, in order to get this **4 times** rotation symetry.

The dihedral angle is given by the formula **cos(angle) = dot(n1,n2)**, with n1 and n2 identifying the normals of the planes of 2 faces rotating.
- we want the angle between the faces to be 90 degres
- as cos(90 degres)=0 we need to solve dot(n1,n2) = 0.

Given there is a 60 degre rotation angle on the vertical axis to get the planes 1 and 2 assembled, we can compute like below.

```
// looking for r
n1 = vec3(-sqrt(3)/2.0,1/2,0)  
n2 = vec3(-cos(r)* sqrt(3)/2,-1/2,-sin(r)*sqrt(3)/2)

dot(n1,n2) = 3/4*cos(r) - 1/4 
```
the dot product simplifies to cos(r)=1/3, meaning 
```
    // Bend angle of approx 70,52877937 degres
    // This is the first key value to build the puzzle
    float r = acos(1./3.);
```

The Wikipedia page about the [Rhombic dodecahedron](https://en.wikipedia.org/wiki/Rhombic_dodecahedron) mention that **arccos(1/3)** is the acute angles on each face. Of course there is the explanation in Stewart Coffin's book **The Puzzling World of Polyhedral Dissections**.

The French version says that it's value is **2*arctan(1/√2)** and it appears that this is the same value. I would be happy to have the explanation of this equivalence. [Wolfram's calculation confirmation](https://www.wolframalpha.com/input/?i=2*arctan%281%2F%E2%88%9A2%29-arccos%281%2F3%29)

```
2*arctan(1/√2)-arccos(1/3) = 0
```

Shadertoy illustration of the arrangement of the sticks on the puzzle.

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/slfSRj?gui=true&t=10&paused=true&muted=false" allowfullscreen></iframe>

90° rotation arrangement visible around the "craters" of the puzzle.

## The Puzzling World of Polyhedral Dissections

With Philippe Cichon's blog, I discovered an incredible book available online for free !

[he rhombic dodecahedron can be totally enclosed by a symmetrical cluster of 12 sticks having equilateral-triangular cross-section](https://johnrausch.com/PuzzlingWorld/chap08.htm). This is the key of the design of this puzzle. There is many variations on it.

The Stewart Coffin's book **The Puzzling World of Polyhedral Dissections** has been made available on the Internet by [John Rausch](https://www.puzzle-place.com/wiki/John_Rausch)

>The Puzzling World of Polyhedral Dissections was obviously not written by Stewart to get rich. Anyone who produces such works does it as a labor of love for a subject that is very dear to them. As puzzle collectors, we owe Stewart a huge debt of gratitude for sharing with us his knowledge about the mathematics, aesthetics and philosophy of geometric puzzles. If you enjoy it as much as I do, drop Stewart a line and thank him for his unselfish gesture.

>So, during a recent visit with Stewart, I asked him what he thought about publishing it on the Internet. I hope you are as happy as I am that he said, "go for it!"

>John Rausch
>Oregonia, Ohio 1998

[PuzzlingWorld By Stewart T. Coffin](https://johnrausch.com/PuzzlingWorld/contents.htm)

## Position the pieces on the Rhombic dodecahedron

![preview](https://sylvain69780.github.io/assets/images/scorpius_puzzle_face1.svg)

Details of the front view of one of the 24 puzzle's pieces.
The diameters of the holes and the pivots can be 6,0 mm, drilling no more than 10,0 mm

|symbol|value|explanation|calculation|
|---|---|---|---|
|trunc|10%|pencentage of trucation of the top of the piece.|free choosen value, adds complexity in the calculations compared to a simple triangular shape.|
|k|1,732|square root of 3, Pythagorean theorem applied to the height of an half equilateral triangle.|sqrt(3)|
|f1|15.0 mm|width of face 1|unit for calculations|
|f2|27.0 mm|width of face 2| 2 * f1 * (1-trunc)|
|f3|1.5 mm|width of face 3| f1 * trunc|
|f4|23.4 mm|width of face 3| f1 * k * (1-trunc) |



![preview](https://sylvain69780.github.io/assets/images/scorpius_puzzle_rhombus.svg) 

Top view of face 1 on the Rhombic dodecahedron rhombus face and developed view of face 2. Face 1 is where most of the magic happens, because it's the contact face this the inner Rhombic Dodecahedron. This is also the location of the pivots that must match an hole on face 2 of the locked neighbouring piece. 

|symbol|value|explanation|calculation|
|---|---|---|---|
|rdan|70,5°| the acute angles on each face of the rhombic dodecahedron|acos(1/3)|
|d1|15,91 mm|half side of the Rhombic face.|f1/sin(rdan)|
|d2|14,32 mm|Corrected (because of truncation) half side of the Rhombic face.|d1 * (1-trunc) *or* (1-trunc) * f1/sin(rdan)|
|slope|35,36%|slope of the bended lines in comparison with an horizontal line. Usefull to compute the point coordonates.|1/tan(rda) *or* 1/(3 * sin(rda))|
|A.x|15,00 mm|x Coordinate of A from the rhombus center. This point can be visualized as the bottom point of the 6 "craters" of the puzzle ! |f1|
|A.y|21,21 mm|y Coordinate of A from the rhombus center.|d1+f1 * slope *or* f1 * (4/3)/sin(rdan)|
|B.x|-7,50 mm|x Coordinate (relative to A) of B, pivot point on face 1.|-f1/2|
|B.y|11,67 mm|y Coordinate (relative to A) of B, pivot point on face 1.|(d2-f1 * slope)/2|
|C.x|13,5 mm|x Coordinate (relative to A) of C, pivot point on face 2.|f2/2|
|C.y|-3,18 mm|y Coordinate (relative to A) of C, pivot point on face 2.|(f2 * slope-d1)/2|


Verification of the calculations using Shadertoy.


<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/Nlf3W2?gui=true&t=10&paused=true&muted=false" allowfullscreen></iframe>

## Is it possible to use polar domain repetition ?

Domain repetition enables to compute a shape only once by defining repetition domains, like a grid for example.  
The polar repetition is based on non-overlapping domains, and the bending of the pieces makes this [impossible](https://www.shadertoy.com/view/slfGDf). But we can use a simple dicotomy to identify the domain by testing the dihedral plans.  
This is in relation with [Wythoff polyhedrons](https://www.shadertoy.com/results?query=tag%3Dwythoff) on Shadertoy.  
We also need to take these plans into account in the ray marching. This is quite complicated but needs to be tried but may be later.

## References

- [Adam Savage's One Day Builds: Rhombic Dodecahedron with Matt Parker!](https://www.youtube.com/watch?v=65r_1TzJXaQ)

![preview](https://johnrausch.com/PuzzlingWorld/images/fig093.gif)

- SDF from yx on Shadertoy

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/Wd2Gzt?gui=true&t=10&paused=true&muted=false" allowfullscreen></iframe>

```cpp
float scene(vec3 p)
{
    // minified version
    p = abs(p);
    p += p.yzx;
    return (max(max(p.x,p.y),p.z)-1.) * sqrt(.5);
    
    // initial version - intersection of 3 planes in a mirrored space
    /*p = abs(p);
    float a = dot(p,normalize(vec3(0,1,1)))-sqrt(2.)*.5;
    float b = dot(p,normalize(vec3(1,0,1)))-sqrt(2.)*.5;
    float c = dot(p,normalize(vec3(1,1,0)))-sqrt(2.)*.5;
    return max(max(a,b),c);*/
}
```

- My illustration on Shadertoy

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/slSGzy?gui=true&t=10&paused=true&muted=false" allowfullscreen></iframe>


