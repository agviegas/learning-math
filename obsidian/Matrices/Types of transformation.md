
We can see transformation matrices as a "mapping" system. It takes an input (generally a point) and returns an output (the transformed point). In mathematical notation: $F(a) = b$.

We can classify transformations according to several criteria. The criteria is not mutually exclusive non hierarchical.

![[Pasted image 20230216013721.png]]

# Linear transformations

A transformation is [[Linear transformations|linear]] if it follows the following 2 conditions:

$$F(a+b) = F(a) + F(b)$$
$$F(ka) = kF(a)$$

This is a fancy way of saying that: 

- If we add two vectors and apply a transform, it should have the same result as applying the transformation to both vectors and then adding them.

- If we scale a vector and then apply a transform, it should have the same result as applying the transform and then scaling it.

There are two very important implications:

>If we take a look at the properties of the [[Matrix operations#Matrix - vector product|vector-matrix product]], we'll see that these two conditions are always true. So, in other words, **any transformation that can be accomplished with a matrix multiplication is a linear transformation**.

>All linear transformations will transform the zero vector into the zero vector. If $F(0) = a | a \neq 0$, then $F$ cannot be a linear mapping, since $F(k0) = a$ and therefore $F(k0) \neq kF(0)$ This means that **linear transformations don't contain translation**.>

# Affine transformations

An **affine transformation** is a [[#Linear transformations|linear transformation]] followed by a translation. Therefore affine transforms are just a superset of linear transforms: all linear are affine, but not all affine are linear. 

# Invertible transformations

A transformation is invertible if there exist an opposite transformation $F^{-1}$ that "undoes" the original transformation $F$. In other words:
$$F^{-1}(F(a)) = F(F^{-1}(a)) = a$$

In mathematical terms, a transformation matrix is invertible if the matrix is itself invertible. 

Intuitively, invertible transformations include **translation**, **rotation**, **scale** and **skewing**, because we can imagine a "reverse transformation" that undoes it. An example of a non-invertible transformation is **projection**, because once we get rid of a dimension, we can't recover that information: it's impossible to "un-project" something without having more information.

# Angle-preserving transformations

A transformation is **angle-preserving** if the angle between two vectors is not altered in magnitude or direction after the transformation. Only **translation**, **rotation** and **uniform scale** are angle-preserving.

# Orthogonal transformations

Orthogonal is a therm used to describe a matrix whose rows form an **orthonormal basis** (a vector basis that is orthogonal to each other and have unit length). They are interesting because it's very easy to compute their inverse, and they are very common to find in practice. 

>All orthogonal transformations are **affine** and **invertible**. Lengths, angles, areas, and volumes are all preserved (although some orthogonal transformations, like reflection, might change the sign of the angles). 

**Translation**, **rotation** and **reflection** are the only orthogonal transformations. The determinant of an orthogonal matrix is ±1.

# Rigid body transformations

A rigid body transformation (also known as **proper transformation**) is a transformation that changes the location and orientation of an object, but not its shape. Lengths, angles, areas, and volumes are all preserved. **Translation** and **rotation** are the only rigid body transformations.

The determinant of a rigid body transformation matrix is 1.