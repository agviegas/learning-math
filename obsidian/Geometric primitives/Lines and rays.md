
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

# 2D lines representations

An infinite 2D line can be expressed with the **slope-intercept** form, which is an **implicit form**:

$$y=mx+y_0$$

- $m$ is the slope of the line, also known as _rise over run_.
- $y_0$ is where the line intercepts the $y$ axis.

![[Pasted image 20230303214449.png|300]]

>This shows that a 2D infinite line only has 2 degrees of freedom: one for rotation and another for translation. 

Vertical lines have infinite slope and can't be represented using this form. Instead, they have the form $x=k$. Horizontal lines have no problem ($m=0$). We can solve this singularity using this slightly different **implicit form**:

$$ax + by = d$$

Nevertheless, this has 3 degrees of freedom, and before we saw that an infinite line could be defined by just two. Therefore, we know that there's some redundancy here. We can make this better if we define the vector $n=[a,b]$, and any point as the vector $p=[x,y]$ we can write that same equation using vector notation and the [[Vector operations#Vector dot product|dot product]]:

$$p \cdot \hat n = d$$

If we _force_ $\hat n$ to be a unit vector, then we get a very interesting interpretation. $n$ just defines the direction of a vector normal to the line, while $d$ defines the **signed distance** of the line to the origin. The signed distance is positive if $d$ is on the same side as $n$. 

>In this form (**normal-distance form**) we are representing a distance and a direction (instead of a point and a direction). In this form we are able to represent all cases, including vertical lines.

![[Pasted image 20230303220546.png|300]]

There are 2 other common ways to represent a line: 

1. As the unit vector $n$ defining the direction and a point $q$ of the line:

$$p \cdot \hat n = q \cdot \hat n$$

![[Pasted image 20230306003028.png|300]]

2. As the perpendicular bisector of 2 points. This is one of the first definitions of a line: the set of two points equidistant from two given points.

![[Pasted image 20230306003217.png|300]]

# 2D lines conversions

Converting between representations is quite easy. Here are some examples (we can also use this to make the reverse conversions):

- Ray defined by 2-points to parametric ray:

$$p_0=p_{org} ~~~~~~~~~d=p_{end}-p_{org}$$

- Parametric ray to ray defined by 2 points:

$$p_{org}= p_0~ ~~~~~~ p_{end}=p_0+d$$

- Parametric ray to implicit line that contains that ray:

$$a=d_y ~~~~~~~~~ b = -d_x ~~~~~~~~~ d=x_{org}~d_y - y_{org}~d_x$$

- Implicit line to slope-intercept form:

$$m=-a/b ~~~~~~~~~~~ y_0=d/b$$

- Implicit line to normal and distance form:

$$\hat n = \frac {[a,b]}{\sqrt{a^2+b^2}} ~~~~~~~~~~~~ distance = \frac{d}{\sqrt{a^2+b^2}}$$

- Point on the line to normal-distance form:

$$distance = \hat n \cdot q$$

- Perpendicular bisector form to implicit form:

$$a=q_y-r_y ~~~~~ b=r_x-q_x$$
$$d=\frac{q+r}{2}\cdot[a,b]=\frac{q+r}{2}\cdot[q_y-r_y~~~~r_x-q_x] = ~...~ =r_xq_y-q_xr_y$$