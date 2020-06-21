---
layout: page
title: Marching Squares
permalink: /articles/Marching-Squares/
---

[Marching Squares](https://en.wikipedia.org/wiki/Marching_squares) (along with its 3D cousin [Marching Cubes](https://en.wikipedia.org/wiki/Marching_cubes)) comes up regularly in discussions of procedural generation.  It can be used to generate pictures like this:

![Marching Squares Example](/images/MarchingSquaresExample.png)

*(the yellow lines are the edges created by the algorithm and the gray is the noise on which the edges are based)*

This looks interesting but what does the algorithm actually do, and what can it be used for?  Let's start with a technical definition:

Marching Squares

: an algorithm that approximates the *isolines*  of a given *isovalue* with respect to some 2D *scalar field*.

Let's unpack this a little.

### What is a Scalar Field?

[Scalar field](https://en.wikipedia.org/wiki/Scalar_field)

: a function that defines a *scalar* (typically a real-number value) at every point in some space.  For example, take this map of a section of Bighorn National Forest in Wyoming:

![Bighorn Map](/images/bighorn.png)

Every point on this 2D map has some elevation associated with it.  Elevation on this map is a scalar field.

### What is an Isoline?

An *[isoline](https://en.wikipedia.org/wiki/Contour_line)* is a line of constant value (the *isovalue*) with respect to some scalar field.  A type of isoline that most people are familar with is a contour line:

![Contour  Line](/images/bighorn-contour.png)

Every point on this line represents 7500 ft of elevation.  If you were standing at any point on this line and walked along it you would always be at an elevation of 7500 ft.  Something else you may have noticed is that contour lines are always loops.  This is not true in general for all spaces or all fields but it's true for elevation on the surface of a globe, and as we shall see, true for our purposes as well.

### So What is Marching Squares Again?

Marching Squares approximates isolines with straight line segments.  It samples a 2D scalar field and uses those samples and some [linear interpolation](https://en.wikipedia.org/wiki/Linear_interpolation) to produce line segments.  For example:

![Marching Squares Shape](/images/marching-shape.png)

Each line segment approximates a small section of the actual contour

 that approximate small sections of isolines for a given isovalue.  If you're using a coherent noise density function like Perlin noise

---
