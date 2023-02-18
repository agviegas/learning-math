Polar coordinate systems can also be used in 3D. The third dimension can be a distance (**cilindrical coordinate system**) or an angle (**spherical coordinate system**).

# Cylindrical coordinates

<img width="300px" src="https://ds055uzetaobb.cloudfront.net/brioche/uploads/WeZLM2hu4C-cylindrical-coordinates.svg?width=500" alt="asdf"/>
Cylindrical coordinates are made simply by adding a third distance dimension called $z$. This way, any point in space can be defined as $(r, \theta, z)$. 

The conversion between this and a cartesian coordinate system is very similar to [[Introduction to polar coordinates|2D polar coordinates]] because the axis Z is just like the cartesian axis Z.

This kind of coordinates are not used very often. They might be useful in cylindrical-like environments or to describe a cylindrical-shaped object. 


# Spherical coordinates

Spherical coordinates systems are created by adding a third angle component $\phi$ . The idea is simple: $r$ is the radius of the sphere and $\theta$ (**azimuth**) and $\phi$ (**zenit**) are angles necessary to describe the positition of that point in the surface of the sphere. 

The traditional spherical coordinate system used in some math / physics books might be a bit inconvenient for us for multiple reasons:

- It is [[Cartesian space|right-handed]], and most 3D apps are coded [[Cartesian space|left-handed]].
- The default horizontal direction $\theta=0$ points in the $+x$ direction (east), which is confusing.
- It would be nice if we could extend 2D polars to 3D polars just by adding a third component 0, like we can do in cartesian coordinates. But unfortunately $(r, \theta)$ is not the same position as $(r,\theta,0)$. In fact, this puts us in **Gimbal lock** position. Having the default $\phi$ to be up is confusing.
- The use of greeks letters can make this confusing.
- It would be nice if the angles for polar coordinates were the same as for **Euler angles**.

Here are some conventions that work better for 3D programming:

- We keep $r$ as the distance.
- $y$ will be up.
- The horizontal angle $\theta$ is renamed $h$ (heading, like a compass heading).
- The vertical angle $\phi$ is renamed $p$ (pitch, measures how much we are looking up or down).
- $h=0$ points to $+z$ (north).
- $p=0$ indicates an horizontal direction.
- We use a [[Cartesian space|left-hand system]], so the positive rotation will be **clockwise** when viewed from above.
- Positive pitch goes down (this is a bit confusing, but it's necessary for the left-hand system).

Spherical coordinates have similar aliasing behavior as [[Introduction to polar coordinates|2D polar coordinates]], and even more cases due to the existance of a second angle. The **canonical form** is also similar, with the addition that $p$ should be between -90º and +90º.

![[Pasted image 20230218011607.png]]

Converting between spherical and cartesian coordinates is easy. The equations for the right-handed and math-like polar system are:

$$x=r~sin(\phi)~cos(\theta)  ~~~~~~~~ y=r~sin(\phi)~sin(\theta)  ~~~~~~~~ z = r~cos(\phi)$$

If we adapt it to our more convenient left-handed system, they will be:

$$x=r~cos(p)~sin(h)  ~~~~~~~~ y=-r~sin(p)  ~~~~~~~~ z = r~cos(p)~cos(h)$$

Converting from cartesian to polar is slightly more complicated due to **aliasing**. We are looking for the **canonical coordinates**. Now, considering our convenient system for 3D, these are the equations:

$$r=\sqrt{x^2+y^2+x^2}  ~~~~~~~~ h = atan2(x, z)  ~~~~~~~~ p=arcsin(-y/r)$$

