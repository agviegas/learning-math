Let's imagine the 2D space $(x,y)$ as existing in 3D in the plane $w=1$. We call that 3D space the **homogeneus space** $(x, y, w)$.

For all points in 3D space that are not in the point $w=1$ we can compute the corresponding 2D point by **projecting** the point onto the plane $w=1$ simply by dividing that point by $w$. That means that any point $(x,y,w)$ can be mapped to the 2D plane like this: $(\frac x w, \frac y w, 1)$ . This is illustrated below.

![[Pasted image 20230216120738.png]]

For any point in that 2D space, there's an infinite number of 3D points that are mapped to that point. That set of infinite points have the form $(kx, ky, k)$ (if $k$ is not 0) and form a straight line illustrated above that goes through the **homogeneus origin**.

>If $w=0$ the division is undefined and there is no corresponding point in the 2D plane. We can interpret a 2D homogeneus point $(x, y, 0)$ as a "point at infinity", which defines a direction (vector) rather than a location (point). 

This same idea applies to 3D as $(x, y, z, w)$, but this is a lot harder to visualize because humans can't see 4D spaces, but it works exactly the same. We can think that the 3D space lies in a 4D hyperplane at $w=1$, and any 4D point can be projected into a corresponding 3D point $(\frac x w, \frac y w, \frac z w, 1)$. 

>Similarly to the 2D case, we can interpret $w=0$ as a point in infinity, or in other words, a direction (vector) rather than a location (point). So all 3D points are usually represented as $(x,y,z,1)$, and all the vectors as $(x,y,z,0)$.

Why is this interesting for us? There are 2 reasons:
- This makes working with [[Affine transformations|translation matrices]] a lot easier.
- If we put the proper value in $w$, the homogeneus division will result in a [[Perspective projection|perspective projection]].