---
layout: post
title: Jobifying Marching Squares
---

My current implementation of [Marching Squares](https://en.wikipedia.org/wiki/Marching_squares) in Unity produces results that look like this:


![Marching Squares Example](/images/MarchingSquaresExample.png)

(the yellow lines are the edges created by the algorithm and the gray is the noise on which the edges are based)

However, this implementation uses features of C# that are not allowed within a Unity Job, such as heap-allocated objects.  I need to re-implement Marching Squares so that it will work with the Job System.  I would also like to parallelize the algorithm so it can take advantage of all those extra cores everyone has in their processors now.

## What Is Marching Squares?

Marching Squares is an algorithm that approximates isolines with respect to some 2D scalar field.

Let's define some terms.

### What is a Scalar Field?

A *[scalar field](https://en.wikipedia.org/wiki/Scalar_field)* is a function that's defines a *scalar* (typically a real-number value) at every point in some space.  For example, take this map of a section of Bighorn National Forest in Wyoming:

![Bighorn Map](/images/bighorn.png)

Every point on this 2D map has some elevation associated with it.  Elevation on this map is a scalar field.

### What is an Isoline?

An *[isoline](https://en.wikipedia.org/wiki/Contour_line)* is a line of constant value (called the *isovalue*) with respect to some scalar field.  A type of isoline that most people are familar with is a contour line:

![Contour  Line](/images/bighorn-contour.png)

Every point on this line represents 7500 ft of elevation.  If you were standing at any point on this line and walked along it you would always be at an elevation of 7500 ft.  Something else you may have noticed is that contour lines are always loops.  This is not true in general for all spaces and fields but it's true for elevation on the surface of a globe, and as we shall see, true for our purposes as well.

### So What is Marching Squares Again?

Marching Squares approximates isolines with straight line segments.  It samples a 2D scalar field and uses those samples and some [linear interpolation](https://en.wikipedia.org/wiki/Linear_interpolation) to produce line segments.  For example:

![Marching Squares Shape](/images/marching-shape.png)

Each line segment approximates a small section of the actual contour

 that approximate small sections of isolines for a given isovalue.  If you're using a coherent noise density function like Perlin noise

## My Implementation

My Marching Squares algorithm uses three distinct steps to produce geometry:

1. Produce edges bound within a bounding rectangle
2. Stitch the edges together into isolines, some of which are incomplete and terminate at the rectangle boundary
3. Connect boundary edges to each other to complete the isolines

Marching Squares produces edges, not polygons.  However, 

---
