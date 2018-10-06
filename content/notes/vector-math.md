+++
title = "Vector Math"
description = "Math utility functions I found helpful with development"
weight = 1
+++

While building games, here are a series of math functions which I found incredibly useful. For the below 
content to be relevant to Unity, you can find the git submodule below:

* [Math-Utils](https://github.com/psuong/math-utils)

# Table of Contents #
* [Vectors](#Vectors)
    * [Basics of Position & Direction](#basics-of-position-direction)
    * [More Fun Things With Direction](#more-fun-things-with-direction)
        * [Direction Relative Of](#direction-relative-of)


# Vectors #
Vectors represent any object which has a magnitude and a position. Consider the cartesian coordinate system 
on a 3D plane which is usually denoted by like the following `(x, y, z)`.

## Basics of Position & Direction ##
A standalone vector can simply represent a point in some space and that's it. To get any other pieces of 
info from that standalone vector, there should be more vectors to derive more info.

Consider two vectors,

* A (-1, 0, 0)
* B (0, 0, 1)

the **direction** from `A -> B` is simply the subtraction of `B - A`, (-1, 0, 1). To get the inverse direction, 
simply reverse the order of subtraction to `A - B`.

```
The formula for getting a direction from a source to a destination is simply:

direction = destination - source
```

Additionally, if we have a point and a direction we can find the source or destination point in the following 
manner.

```
Finding the source:
source = destination - direction

Finding the destination:
destination = source + direction
```

## More Fun Things With Direction ##
Now that the basics are out of the way we can do more complicated things with direction. Imagine building an 
in-game agent which has to steer towards a particular direction.

Given **2** directions, we can find the angle between them (additionally, this means that we supposedly have 3+ 
positions used to calculate the **2** directions).

This is usually denoted by the following:

```
cos (theta) = (A . B) / (||A|| + ||B||)
```

where,

* `A` and `B` is a directional vector
* `.` means the [dot product](https://en.wikipedia.org/wiki/Dot_product) of the two vectors
* `||A||` and `||B||` means the magnitude of the vectors `A` and `B`

When getting the value `theta`, do note that theta is in **radians**. Since, it is easier to think in terms of 
 °, we can multiply:

```
degrees = (theta) * 180/PI
```

{{% notice note %}}
The angle returned is most likely an acute angle, meaning the range is between 0° and 180°. So, an 
angle of **270°** will return **90°**.
{{% /notice %}}

### Direction Relative Of ###
Imagine having a chair to the left of you, you know the chair is clearly left of you because it's next to your 
left hand. Now if you turned 90° to the right, is the chair still left of your relative forward? No, it's 
now behind you. Using this concept, we can determine the relative direction of a destination to its source in
**local space**.

If we use the aforementioned formula stated above, we can just get an acute angle, since 270° is really just 
-90°. Of course, we can try to modify the math to convert -90° to 270°, or we can just determine the sign 
to make determining the relative direction less complicated. To do this, we need the:

* cross product
* dot product

With two directions, by finding the cross product we determine a vector perpendicular two the directions. As such, 
determining the dot product between a normal vector and the perpendicular vector will determine the sign.

{{% notice note %}}
Dot products returns a scalar value from two vectors. When a dot product is:

* 0, then we know that the direction and the normal is perpendicular.
* 1, then we know that the angle between the direction and the normal is less than 90 degrees.
* -1, then we know that the angle between the direction and the normal is greater than 90 degrees.
{{%/ notice %}}

The pseudocode of a function can be written as below to help determine if a position in 3D space is left, right, 
forward, or backward of a relative forward direction.

```
int GetRelativeDirection(vector3 forward, vector3 direction, vector3 normal) {
    var perpendicular = cross(forward, direction);
    var relativeDirection = dot(perpendicular, normal);

    var sign = 0;

    if (relativeDirection > 0.0)
        sign = 1;
    else if (relativeDirection < 0f)
        sign = -1;

    return sign;
}
```

Therefore a position left of the forward would return as -1 and a position right of the forward would return as 1.

{{% notice warning %}}
Visualizations of these transformations are coming! I just need more time to compile it and create gifs.
{{%/ notice %}}
