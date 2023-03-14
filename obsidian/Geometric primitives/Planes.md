A plane is a flat infinite 2D surface. They are very common in 3D and videogames. 

>We could define a plane just like we define a [[Lines and rays#2D lines representations|line in 2D]]: the set of all points that are equidistant from 2 given points. This makes sense because we could think of a plane as the set of infinite 2D lines contained in it (eg. all the threads of a fabric). Similarly to lines in 2D, planes also **divide the space into 2 subspaces**.


Just like [[Lines and rays|lines]], the implicit equation of a plane can be given in scalar notation or vector notation.

$$ax+by+cz=d$$
$$p \cdot n=d$$
 
- The vector $n=[a,b,c]$ is the orientation of the plane. It is called the plane **normal** because it is perpendicular (normal) to the plane. It is often [[Vector operations#Vector normalization|normalized]], but not necessarily. 

-  $d$ describes the position of the plane. More specifically, it's the signed distance to the plane from the origin, measured in the direction of the normal. Increasing $d$ slides the plane in the direction of the normal. If $d<0$, the origin is on the front side of the plane, while $d>0$ means that it's on the backside and $d=0$ means that the plane hits the origin.

>There's only one plane that go through 2 lines. Therefore, we can also describe a plane from **three non-colinear points**. If they were colinear they would be on the same line, and there's infinite planes that go through a single line.

We will assume  a [[Cartesian space|left-handed system]] and that the 3 points $p_1$, $p_2$ and $p_3$ are given in clockwise order looking at them from the positive side of the plane. 

![[Pasted image 20230314000853.png|300]]

To find out $n$ we will simply define 2 vectors from the three points and then make the [[Vector operations#Vector cross product|cross product]], which results in a perpendicular vector. The resulting vector is not necessarily normal, so we also need to normalise it. The edges are going to be called $e$, with a subindex that is different from the subindices of the 2 points that define it.

$$e_3 = p_2 - p_1 ~~~~~~~ e_1 = p_3 - p_2 ~~~~~~~ \hat n = \frac {e_3 \times e_1}{||e_3 \times e_1||}$$

We can extend this to the following formulas to find out $n$:

$$n_x = (z_1+z_2)(y_1-y_2)$$
$$n_y = (x_1+x_2)(z_1-z_2)$$
$$n_z = (y_1+y_2)(x_1-x_2)$$
$$\hat n = \frac{[n_x~~n_y~~n_z]}{\sqrt{n_x^2+n_y^2+n_z^2}}$$

>Now we can simply compute $p$ as the dot product of one of the points and $\hat n$.


# Plane for more points

Sometimes we want to get a plane for more than 3 points that are not quite coplanar (e.g. the vertices of a polygon). The naif approach would be taking 3 random points to compute the plane, but that can have many problems: 

- The vertices could be colinear which would make it impossible to define a plane.
- The vertices could be almost colinear, which would reduce the accuracy of the result.
- The vertices could be very close to each other, reducing the accuracy of the resuult.
- If the points define a concave shape, we could choose vertices that "flip" the triangle defined by them and end up with the wrong normal direction.

It turns out that a very reliable method to find out the best fit plane is to make the "average" between all the triplets of points, starting from $(p_1,p_2,p_3)$, then $(p_2,p_3,p_4)$, then $(p_4,p_5,p_6)$ and so on. We can do this efficiently just adding all $n$, and in the end normalizing the result to get $\hat n$.

$$n_x=(z_1+z_2)(y_1-y_2)+(z_2+z_3)(y_2-y_3)+...$$
$$n_y=(x_1+x_2)(z_1-z_2)+(x_2+x_3)(z_2-z_3)+...$$
$$n_z=(y_1+y_2)(x_1-x_2)+(y_2+y_3)(x_2-x_3)+...$$

This can be expressed succintly with summation notation.

$$n_x=\sum_{i=1}^n(z_i+z_{i+1})(y_i-y_{i+1})$$
$$n_y=\sum_{i=1}^n(x_i+x_{i+1})(z_i-z_{i+1})$$
$$n_z=\sum_{i=1}^n(y_i+y_{i+1})(x_i-x_{i+1})$$
Similarly, the best fit $d$ value can be computed as the average value for each point:

$$d=\frac 1 n \sum_{i=1}^n(p_i \cdot n) = \frac 1 n (\sum_{i=1}^np_i)  \cdot n$$
The code to compute $\hat n$ looks like this:

```c
Vector3 computeBestFitNormal(const Vector3 v[] , int n) {
	// Zero out sum
	Vector3 result = kZeroVector;

	// Start with the ‘‘previous’’ vertex as the last one
	// This avoids an if−statement in the loop
	const Vector3 ∗ p = &v [n−1];
	
	// Iterate through the vertices
	for (int i = 0; i < n; ++i) {
		// Get shortcut to the ‘‘current’’ vertex
		const Vector3 ∗c = &v[i];
		// Add in edge vector products appropriately
		result.x += (p−>z + c−>z) ∗ (p−>y − c−>y);
		result.y += (p−>x + c−>x) ∗ (p−>z − c−>z);
		result.z += (p−>y + c−>y) ∗ (p−>x − c−>x);
		
		// Next vertex, please
		p = c;
	}
	
	// Normalize the result and return it
	result.normalize();
	return result;
}
```


# Point-plane distance

![[Pasted image 20230314005125.png|300]]

A common situation in 3D software is to have a point $q$ that is not in the plane, and we want to know its signed distance to the plane (positive if it's in the front, negative if it's in the back).

The distance from $q$ to the plane is defined by a line perpendicular to the plane. That line intersects with the plane in $p$, which is the point in the plane closest to $q$. As it's perpendicular to the plane, the vector from $p$ to $q$ can be expressed as $a \hat n$, where $a$ is the signed distance we are looking for.

It turns out that we can find out $a$ without knowing the location of $p$ with simple algebra and the basic plane equation in vector form that we saw at the beginning ($p ~\hat n = d$). Remember that $\hat n \hat n = 1$ because the dot product of a normal vector by itself is always 1.

$$p+a\hat n = q \rightarrow p\hat n + a \hat n \hat n = q\hat n \rightarrow d+a = q\hat n \rightarrow a = q\hat n - d$$