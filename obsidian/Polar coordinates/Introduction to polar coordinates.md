The [[Cartesian space|cartesian coordinate system]] is not the only way to define things in space accurately.

The polar coordinate system is actually very simple. It has an **origin** (or **pole**) and a single axis. Any point in 2D space can be defined with:

- A **length** $r$ from the origin to the point (positive or negative).
- An **angle** $\theta$ that starts at 0 in the direction $+x$ and increments counter-clockwise.

<img width="300px" src="https://mathinsight.org/media/image/image/polar_coordinates.png" alt="asdf"/>

>Just like cartesian systems sometimes represent a gridSome polar coordinate system representation have a grid that represent $r$ as circles and some values of $\theta$ as radial lines.

>In cartesian coordinate systems, units doesn't matter: whatever we represent just gets bigger or smaller. But in a polar coordinate system, changing the $r$ units can produce drastically distorted results.

In cartesian coordinate systems there is only a way of defining a point in space, but that's not the case in polar coordinate systems. For instance, the point $(1, -180º)$ is the same as $(1, 180º)$, $(r, 540º)$, etc. So there are  an infinite number of polar pairs that can be used to describe a point. This phenomenom is known as **aliasing**. 

Two pairs of coordinates are said to be **aliases** to each other if they have different numeric values but refer to the same point in space. For any pair of polar coordinates $(r, \theta)$, we can define all their aliases like this (with $k$ being an integer):

$$((−1)^kr, \theta + k180º)
,$$

The **canonical** coordinates for a point are the only possible coordinates where:

- $r \geq 0$ 
- $\theta \in a(-180º, 180º]$ (the interval is half open because -180º is never used).
- $r=0 \rightarrow \theta = 0$

We can convert any polar coordinates to canonical simply by:

- If $r$ is negative, make it positive and add 180º to $\theta$.
- If $r=0$, then make $\theta=0$.  
- If $\theta$ is more than 180º, subtract 360º until it is less or equal.
- If $\theta$ is less than -180º, add 360º until it is more.

<img width="300px" src="https://keisan.casio.com/keisan/lib/real/system/2006/1223527679/PolarCartesian.gif
" alt="asdf"/>

Converting from polar to cartesian is easy. We just need to apply [[Trigonometry|basic trigonometry]]. 

$$x = r ~cos(\theta)$$
$$y = r ~sin(\theta)$$
This works for any pair of polar coordinates, not just the canonical ones. Now, to convert from cartasian to canonical polar coordinates we can simply apply [[Trigonometry|Pithagoras]]:

$$r=\sqrt{x^2+y^2}$$

Now, for computing $\theta$ we could be tempted to try $\theta=atan(\frac y x)$, but this has two problems:

- Division at x=0 is undefined.
- The range of that function is just $[-90º, +90º]$. The problem is that the division y/x discards useful information about the original signs of x and y, so it doesn't work for  other quadrants.

In the default math library of most programming languages we have the function $atan2$, which handles all the quadrants (**we still need to handle the x=0 case manually with an if statement for most programming languages**). This is how to do it by hand:

```
if(x = 0, y = 0)  theta = 0
if(x = 0, y > 0)  theta = 90º
if(x = 0, y < 0)  theta = -90º
if(x > 0)         theta = atan(y/x)
if(x < 0, y >= 0) theta = atan(y/x) + 180º
if(x < 0, y < 0) theta = atan(y/x) - 180º
```



