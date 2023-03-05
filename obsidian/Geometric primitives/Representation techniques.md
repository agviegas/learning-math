There are multiple strategies to define geometric shapes in space. Different techniques are useful in different situations. 

# Implicit form

We can define an object in **implicit form** by defining a Boolean function $f(x,y,z)$ that is true for all points of the primitive and false for the rest of points in space. For example, the following equation:

$$x^2+y^2+z^2=1$$
is true for all the points in the surface of a unit sphere at the origin. Another examples of common implicit equations are: 

**Conic sections** 

Results of cutting a cone with a plane: circle, ellipse, parabola and hyperbola), which have the form $Ax^2+Bxy+Cy^2+D=0$. 

**Metaballs** 

They are an implicit method used to describe fluids and organic shapes. We can convert implicit organic shapes like this into polygonal meshes using the algorithms like the **marching cubes**.

# Implicit form

The primitive is described with a function but the spatial coordinates are not the input, but the output. For instance, we can define the following functions:

$$x(t) =\cos 2\pi t ~~~~~~~~ y(t) =\sin 2\pi t$$
The argument $t$ is known as the _parameter_ and is independent from the coordinate system. In this case, as $t$ goes from zero to one, the point $[x(t), y(t)]$ traces a circle. It's often convenient to normalize $t$ to go have the range $[0, 1]$ (or also $[0, l]$, where $l$ is some measure length of the primitive).

>Functions that depend only of one parameter are called **univariate** and draw a curve. Functions that depend on two parameters are **bivariate** and draw a curve.

>It's often convenient to normalize $t$ to go have the range $[0, 1]$ (or also $[0, l]$, where $l$ is some measure length of the primitive).


# Straighforward form

This includes all the ad-hoc methods to express a geometry through its most important and obvious information. For instance, we could describe a line segments through its two endpoints, or we could describe a sphere by its center and its radius.


# Number of degrees of freedom

Regardless of the representation method, each geometric primitive has a **number of degrees of freedom**. This is the minimum number of properties necessary to describe the primitive unambiguously. It's interesting that for some primitives, different representations have different numbers, and that's because of the "redundancy" of the parametrization, which could be eliminated by applying appropiate constraints.

For example, if we express a 2D circle with its **parametric equation**, we have 3 degrees of freedom: $x_c$ and $y_c$ for the center and $r$ for the radius:

$$x(t) =x_c+r \cos 2 \pi t ~~~~~~~~~~~ y(t) =y_c + r \sin 2 \pi t$$

But if we express this as the general conic section equation ($Ax^2+Bxy+Cy^2+D=0$), we get 4 degrees of freedom. But if we make it specific to the circle, we get back to 3 degrees. Generally, a conic section equation is considered to be a circle if it can be expressed like this. This is known as the **implicit equation** of the circle:

$$(x-x_c)^2+(y-y_c)^2=r^2$$

