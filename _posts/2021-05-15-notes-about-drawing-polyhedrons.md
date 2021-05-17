---
layout: default
title: "Notes about drawing polyhedrons"
tags: shadertoy
---

Drawning polyhedrons is quite cool, and these 3D shapes have something facinating, I would make an exception for the CUBE that is very commonly in our daily life, but still very usefull !

Let's start with [Ray marching starting point](https://shadertoy.com/view/WtGXDD) from BigWings, who precisely is drawing a cube.

I first looked at [IQ's SDF page](https://iquilezles.org/www/articles/distfunctions/distfunctions.htm) and [Mercury library](http://mercury.sexy/hg_sdf/) and it's unofficial [port on Shadertoy](https://www.shadertoy.com/view/Xs3GRB)

The more classical way to do 3D is to define a [Mesh](https://www.scratchapixel.com/lessons/3d-basic-rendering/introduction-polygon-mesh).  
IQ did it in a pixel shader [here](https://www.shadertoy.com/view/4slGzn) and Fabrice a tool to load meshes encoded in images [here](https://www.shadertoy.com/view/Wsy3DG). 

# Cube

The exact SDF is simple, and there is an IQ's video on how to get it by yourseft.
Even more simple but not exact is to just take the MAX of the distance to each face (fBoxCheap in Mercury library)

- IQ's [box fonction](https://iquilezles.org/www/articles/distfunctions/distfunctions.htm) 

# Octahedron 

I tried to understand the Cheap IQ function below using [Desmos](https://www.desmos.com/calculator/ovavcqosu8)  
This is derived from the distance to a plan, that is dot(p,n) + h (on the same page)
Here the plan normal n is vec3(1), to get it normalized there is this divided by 0.57735027 that is 1/sqrt(3).
By taking the absolute value of each coordinate, the function need to take care of only 1 plan instead of 8.
If I understand well, the distance is not too much over estimated, the maximum is sqrt(3) times the euclidian distance.

```c
float sdOctahedron( vec3 p, float s)
{
  p = abs(p);
  return (p.x+p.y+p.z-s)*0.57735027;
}
```
