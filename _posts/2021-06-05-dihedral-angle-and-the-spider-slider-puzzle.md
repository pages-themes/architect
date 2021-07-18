---
layout: default
title: "Dihedral angle and the scorpius spider slider puzzle"
tags: shadertoy
---

# Dihedral angle and the scorpius spider slider puzzle
## What is this ?

When I was a child, I had the chance to own a "scorpius slider spider puzzle", a piece of wood art bought 30 years ago.

![preview](https://static.blog4ever.com/2008/06/213622/artfichier_213622_8769121_202010012502419.png)

I learnt reading [Philippe Cichon's blog (French)](https://puzzles-et-casse-tete.blog4ever.com/le-scorpius-1) that it's a rare puzzle, very few makers exists.

The shape is very cool and I tried to reproduce it on Shadertoy. For this I needed to understand the geometry in place here, with only my elementary knowledge. 

This video of Philippe Cichon shows how to mount and unmout it (in French)
[Le Scorpius on Youtube](https://www.youtube.com/watch?time_continue=13&v=2orJ6rTSx2s&feature=emb_logo)

## Calculation of the angle to bend the pieces : The Dihedrial angle

What fascinated me is the rotation angle needed to bend each little piece when mounting the puzzle.

Refering to the article on [Philippe Cichon's blog (French)](https://puzzles-et-casse-tete.blog4ever.com/le-scorpius-1), this bend angle is 70 degres, but why this value ?  
All pieces have a triangular section, with angles 30, 60 and 90 degres, this is an half equilateral triangle with sides 1,2,sqrt(3), but when assembled, all 4 pieces are connected with a polar symetry of 90 degres around a central point.

I suspected that 70 degres was not an exact value, and wanted to compute it by myself using some basic geometry. It was not so easy.

![faces numbers](https://static.blog4ever.com/2008/06/213622/artfichier_213622_8769120_202010011725351.png)

A [dihedral angle](https://mathworld.wolfram.com/DihedralAngle.html) is the angle between two intersecting planes

![preview](https://sylvain69780.github.io/assets/images/scorpius_puzzle_angle.svg)

When assembled, the Dihedral angle of the planes of one pieces with the next one should be 90 degres, in order to get this **4 times** rotation symetry.

The dihedral angle is given by the formula **cos(angle) = dot(n1,n2)**, with n1 and n2 identifying the normals of the planes of 2 faces rotating.
- we want the angle between the faces to be 90 degres
- as cos(90 degres)=0 we need to solve dot(n1,n2) = 0.

Given there is a 60 degre rotation angle on the vertical axis to get the planes 1 and 2 assembled, we can compute that 

![preview](https://sylvain69780.github.io/assets/images/dihedral_faces.png)

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

>I found interesting that the Wikipedia page speaking about the [Rhombic dodecahedron](https://en.wikipedia.org/wiki/Rhombic_dodecahedron) mention that **arccos(1/3)** is the acute angles on each face. Of course there is the explanation in Stewart Coffin's book **The Puzzling World of Polyhedral Dissections**.

The French version says that it's value is **2*arctan(1/√2)** and it appears that this is the same value. I would be happy to have the explanation of this equivalence.

```
2*arctan(1/√2)-arccos(1/3) = 0
```

[Wolfram's calculation confirmation](https://www.wolframalpha.com/input/?i=2*arctan%281%2F%E2%88%9A2%29-arccos%281%2F3%29)

## Position the pieces on the Rhombic dodecahedron

    float edge = (1.0/sin(r/2.0))*.5;  // length of the edge of the rhombus 
    float scale = edge*cos(PI/2.0-r); // base of the equilateral triangle

    

## Position of the contact surfaces and pin point on each face

Compute the bend angle between two pieces is good but not enough.

One can find on [this schema](https://sylvain69780.github.io/assets/images/scorpius_puzzle.svg) the calculations using painfull but basic trigonomerty formulas.

![preview](https://sylvain69780.github.io/assets/images/scorpius_puzzle.svg)

And it works !

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/Nlf3W2?gui=true&t=10&paused=true&muted=false" allowfullscreen></iframe>


## Is it possible to use polar domain repetition ?

Domain repetition enables to compute a shape only once by defining repetition domains, like a grid for example.  
The polar repetition is based on non-overlapping domains, and the bending of the pieces makes this [impossible](https://www.shadertoy.com/view/slfGDf). But we can use a simple dicotomy to identify the domain by testing the dihedral plans.  
This is in relation with [Wythoff polyhedrons](https://www.shadertoy.com/results?query=tag%3Dwythoff) on Shadertoy.  
We also need to take these plans into account in the ray marching. This is quite complicated but needs to be tried but may be later.

## The Puzzling World of Polyhedral Dissections

With Philippe Cichon's blog, I discovered an incredible book available online for free.

This is the story of the Stewart Coffin's book **The Puzzling World of Polyhedral Dissections** made available on the Internet by [John Rausch](https://www.puzzle-place.com/wiki/John_Rausch)

>The Puzzling World of Polyhedral Dissections was obviously not written by Stewart to get rich. Anyone who produces such works does it as a labor of love for a subject that is very dear to them. As puzzle collectors, we owe Stewart a huge debt of gratitude for sharing with us his knowledge about the mathematics, aesthetics and philosophy of geometric puzzles. If you enjoy it as much as I do, drop Stewart a line and thank him for his unselfish gesture.

>So, during a recent visit with Stewart, I asked him what he thought about publishing it on the Internet. I hope you are as happy as I am that he said, "go for it!"

>John Rausch
>Oregonia, Ohio 1998

[PuzzlingWorld By Stewart T. Coffin](https://johnrausch.com/PuzzlingWorld/contents.htm)

[he rhombic dodecahedron can be totally enclosed by a symmetrical cluster of 12 sticks having equilateral-triangular cross-section](https://johnrausch.com/PuzzlingWorld/chap08.htm). This is the key of the design of this puzzle. There is many variations on it.

## More about the Rhombic Dodecahedron

If you want to build a fantastic light using this geometric shape have a look at the youtube video below.

[Adam Savage's One Day Builds: Rhombic Dodecahedron with Matt Parker!](https://www.youtube.com/watch?v=65r_1TzJXaQ)

![preview](https://johnrausch.com/PuzzlingWorld/images/fig093.gif)

Using this SDF from yx, I can verify that. 

[Rhombic Dodecahedron SDF](https://www.shadertoy.com/view/Wd2Gzt)

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

I published the animation showing this neat fact and was happy to get some likes.  

I also made an effort to extensibly comment the code, taking Shane as reference for the formatting.

**Rhombic Dodecahedron Enclosing**

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/slSGzy?gui=true&t=10&paused=true&muted=false" allowfullscreen></iframe>


