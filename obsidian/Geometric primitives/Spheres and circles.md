A sphere is the set of 3D points that are a fixed distance (**radius**) from a given point (**center**). In fact, the **straightforward representation** of a sphere is simply its radius and its center.

>They are common in 3D applications because of their simplicity. For instance, they are used as simple bounding boxes because the equations for intersection with other spheres are very simple. Unlike **bounding boxes**, rotation doesn't change it, so it ignores the rotation of the object it contains. 

The implicit equation of a sphere of radius $r$ and center $c$ is really simple: 

$$||p-c|| = r$$
- $p$ is any point on the surface of the sphere.
- For any point inside the sphere, we can simply substitute $=$ by $<=$.
- This equation uses vector notation, so it also works for a definition of a circle in 2D.

A more common form of this equation is to expand the vector notation and square both sides (so that we get rid of the negative results).

- For a 2D circle:
$$(x - c_x)^2+(y-c_y)^2=r^2$$
- For a 3D sphere:

$$(x-c_x)^2+(y-c_y)^2+(z-c_z)^2=r$$

With elementary geometry, we can also easily get the formulas of some properties. It's interesting to notice that the derivative of the area of the circle is its circumference, while the derivative of the volume of a sphere is its surface area.

- Diameter: $D=2r$
- Circumference: $C=2\pi r = \pi D$
- Area of a circle: $A=\pi r^2$
- Surface area of a sphere: $S=4 \pi r^2$
- Volume of a sphere: $V= \frac 4 3 \pi r^3$

