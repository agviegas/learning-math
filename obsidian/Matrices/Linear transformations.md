A **linear transformation** is a transformation that preserves straight and parallel lines and that has **no translation** (the origin does not move). A transformation that has translation is an [[Affine transformations|affine transformation]].

Knowing that [[Introduction to matrices#Geometric definition|the rows of a transformation matrix are the axis of the transformed coordinate system]], we can express any transformation as a matrix by checking what happens to the **standard basis vectors** $i$, $j$, $k$ as a result of the transformation.

# Rotation

Rotations in 2D can only happen around a point, and the only parameter needed is the angle $\theta$. Generally, counter-clockwise is considered positive rotation. The basis vectors have a length of 1, so we can use using [[Trigonometry|simple trignonometry]] to define the positions of $p'$ and $q'$ in a unit circle depending on $\theta$.

$$R= \begin{bmatrix} p \\ q\end{bmatrix} = \begin{bmatrix} cos(\theta) & sin(\theta) \\ -sin(\theta) &  cos(\theta)\end{bmatrix}$$

![[Pasted image 20230210151327.png]]



Rotation in 3D follows the same logic as 2D, but instead of rotating around a point, we will rotate around an axis. Actually, in 2D we are rotating around the "z" axis, although we never see it. 

Applying exactly the same logic and the [[Cartesian space|left hand rule]], we can infere the following transformation matrices for each axis. It's noticeable that the matrix row that represents the axis where we apply the rotation doesn't change.

$$R_x= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix}1 & 0 & 0 \\0 & cos(\theta) & sin(\theta) \\ 0 & -sin(\theta) &  cos(\theta)\end{bmatrix}$$
$$R_y= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix}cos(\theta) & 0 & -sin(\theta) \\0 & 1 & 0 \\ sin(\theta) & 0 &  cos(\theta)\end{bmatrix}$$
$$R_z= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix}cos(\theta) & sin(\theta) & 0 \\ -sin(\theta) & cos(\theta) & 0 \\ 0 & 0 &  1 \end{bmatrix}$$

>Although we are working with [[Cartesian space|left hand convention]], these matrices would work also for right hand systems because of the positive rotation definition for each system.


# Scale

Scaling an object means making it proportionally bigger or smaller by a factor of $k$. There are 3 possibilities:

- $k > 1$ : the object gets bigger in that dimension.
- $1 > k > 0$ : the object gets smaller in that dimension.
- $k = 0$ : the objects gets **projected ortographically**.
- $k < 0$ : the objects get **reflected**.

This point will only cover $k > 0$. Using the same intution as for rotation, it's easy to determine that the scale transformation matrix in 2D looks like this:

$$S= \begin{bmatrix} p \\ q\end{bmatrix} = \begin{bmatrix} k_x & 0 \\ 0 &  k_y\end{bmatrix}$$

And the 3D scale transformation matrix si very similar:

$$S= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix} k_x & 0 & 0 \\ 0 &  k_y & 0 \\ 0 &  0 & k_z\end{bmatrix}$$

For instance, if we multiply an arbitrary vector by this matrix, we'll get the expected result: each dimension has been multiplied by the corresponding $k$ component!

$$\begin{bmatrix} x & y & z\end{bmatrix} \begin{bmatrix} k_x & 0 & 0 \\ 0 &  k_y & 0 \\ 0 &  0 & k_z\end{bmatrix} = \begin{bmatrix} x k_x & y k_y & z k_z\end{bmatrix}$$

# Orthographic projection

The term _projection_ refers to any operation that gets rid of one dimension. 

- In 2D, we can project into a line (1D).
- In 3D we can project into a plane (2D).

One way to do this is to apply a [[#Scale|scale]] with one of the components of $k$ being zero. 

>This is also called **parallel** projection because the coordinate system is transformed using parallel lines. A very common alternative is a **perspective projection**.

Projecting in the cardinal axis (2D) or planes (3D) is actually quite easy. We just need to get rid of the dimension that is parallel to the direction of projection (or, in other words, orthogonal to the projected axis or plane). This is how it looks like in 2D:

$$P_x= \begin{bmatrix} p \\ q\end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 &  0\end{bmatrix}$$
$$P_y= \begin{bmatrix} p \\ q\end{bmatrix} = \begin{bmatrix} 0 & 0 \\ 0 &  1\end{bmatrix}$$

And this is how it looks like in 3D:

$$P_{xy}= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\ 0 &  1 & 0 \\ 0 &  0 & 0\end{bmatrix}$$
$$P_{xz}= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\ 0 &  0 & 0 \\ 0 &  0 & 1\end{bmatrix}$$
$$P_{yz}= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix} 0 & 0 & 0 \\ 0 &  1 & 0 \\ 0 &  0 & 1\end{bmatrix}$$

# Reflection

Reflection or mirroring is an operation that "flips" the object about a line (2D) or a plane (3D). It's the same as scaling using a $k$ where one of the factors is negative. It's important to notice that objects can only be reflected once. 

If we reflect it again (even if it's about a different axis or plane), the result will be the original object (probably rotated / moved somewhere else).


# Shearing

![[Pasted image 20230216002807.png]]

Shearing or Skewing is an operation that "skews" the coordinate space, streching it non uniformly. Angles are not preserved, but areas and volumes are. This operation is not very common by itself, although it's smartly used to make [[Affine transformations#4x4 translation matrices|translations]].

The basic idea is to add a multiple of one coordinate to the other. The shearing in 2D are the following, where $s$ is the shear factor in that coordinate:

$$H_x(s)= \begin{bmatrix} p \\ q\end{bmatrix} = \begin{bmatrix} 1 & 0 \\ s &  1\end{bmatrix}$$
$$H_y(s)= \begin{bmatrix} p \\ q\end{bmatrix} = \begin{bmatrix} 1 & s \\ 0 &  1\end{bmatrix}$$

The coordinate where we apply the shear will increment proportionally to the other axis and the $s$ factor. For instance, applying the same share as the image above to a generic vector:

$$\begin{bmatrix} x & y\end{bmatrix} \begin{bmatrix} 1 & 0 \\ s &  1\end{bmatrix} = \begin{bmatrix} x + ys & y\end{bmatrix}$$

The shear matrices in 3D are very similar but using 2 factors, one per non-sheared dimension:

$$H_{xy}(s,t)= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\ 0 &  1 & 0 \\ s &  t & 1\end{bmatrix}$$
$$H_{xy}(s,t)= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\ s &  1 & t \\ 0 &  0 & 1\end{bmatrix}$$
$$P_{xy}(s,t)= \begin{bmatrix} p \\ q \\ r\end{bmatrix} = \begin{bmatrix} 1 & s & t \\ 0 &  1 & 0 \\ 0 &  0 & 1\end{bmatrix}$$
