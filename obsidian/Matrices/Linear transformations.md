A **linear transformation** is a transformation that preserves straight and parallel lines and that has **no translation** (the origin does not move). A transformation that has translation is an [[Affine transformations|affine transformation]].

Knowing that [[Introduction to matrices#Geometric definition|the rows of a transformation matrix are the axis of the transformed coordinate system]], we can express any transformation as a matrix by checking what happens to the **standard basis vectors** $i$, $j$, $k$ as a result of the transformation.


# 2D Rotation

Rotations in 2D can only happen around a point, and the only parameter needed is the angle $\theta$. Generally, counter-clockwise is considered positive rotation. The basis vectors have a length of 1, so we can use using [[Trigonometry|simple trignonometry]] to define the positions of $p'$ and $q'$ in a unit circle depending on $\theta$.

$$M= \begin{bmatrix} p \\ q\end{bmatrix} = \begin{bmatrix} -sin(\theta) & cos(\theta) \\ cos(\theta) &  sin(\theta)\end{bmatrix}$$

![[Pasted image 20230210151327.png]]


# 3D Rotation

