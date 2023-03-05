
Linear segments are the most basic geometric representation. There are 3 types:

- **Line**: straight sequence of points that extends in both directions into the infinity.
- **Line segment**: finite portion of a line that has 2 segments.
- **Ray**: a line segment with a direction.

# Rays

So a ray has an origin, an endpoint, a length and (unless the length is zero) a direction. Rays are of fundamental importance in 3D apps and videogames: they are everywhere.



The most obvious way to define  ray is the **straightforward form**: an **origin** and an **endpoint**:

$$\begin{bmatrix} p_{org} & p_{end}  \end{bmatrix}$$
>Rays have $2n$ degrees of freedom, with $n$ being the number of dimension it has. In 2D, a ray has 4 degrees of freedom: the $[x,y]$ coordinates for the origin and the endpoint. In 3D, we add $z$ to both points, so it's 6 degrees of freedom.

The **parametric form** is only slightly different:

$$p(t) = p_0 + t \vec d$$

- $p_0$ is the origin.
- $\vec d$ contains both the direction and the length. 
- The parameter $t$ has the range $[0, 1]$.

An common alternative is to make $\vec d$ a unit vector and make $t$ range $[0, l]$, with $l$ being the length of the ray.

# 2D lines

An infinite 2D line can be expressed with the **slope-intercept** form, which is an **implicit form**:

$$y=mx+y_0$$

- $m$ is the slope of the line, also known as _rise over run_.
- $y_0$ is where the line intercepts the $y$ axis.

![[Pasted image 20230303214449.png|300]]

>This shows that a 2D infinite line only has 2 degrees of freedom: one for rotation and another for translation. 

Vertical lines have infinite slope and can't be represented using this form. Instead, they have the form $x=k$. Horizontal lines have no problem ($m=0$). We can solve this singularity using this slightly different **implicit form**:

$$ax + by = d$$

Nevertheless, this has 3 degrees of freedom, and before we saw that an infinite line could be defined by just two. Therefore, we know that there's some redundancy here. We can make this better if we define the vector $n=[a,b]$, and any point as the vector $p=[x,y]$ we can write that same equation using vector notation and the [[Vector operations#Vector dot product|dot product]]:

$$p \cdot n = d$$

If we _force_ $n$ to be a unit vector, then we get a very interesting interpretation. $n$ just defines the direction of a vector normal to the line, while $d$ defines the **signed distance** of the line to the origin. The signed distance is positive if $d$ is on the same side as $n$. 

![[Pasted image 20230303220546.png|300]]