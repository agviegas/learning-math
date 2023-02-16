There is a special operation for **square matrices** called **inverse**. It is very useful and is present everywhere in 3D software.

# Math interpretation

The inverse of a square matrix $M$ is denoted as $M^{-1}$ , and is a matrix such that:

$$M(M^{-1}) = I$$

Not all matrices have an inverse. An easy example is a matrix with a column or row filled with zeros. No matter what we multiply the matrix by, the corresponding row or column in the result will also be filled with zeros.

>Matrix that have an inverse are called **invertible** or **nonsingular**. A matrix that doesn't have an inverse is called **noninvertible** or **singular**.

Invertible matrices have the following properties:

- All the columns and all the rows are **linearly independent**.
- The equation $\vec v M = 0$ is true only if $\vec v = 0$.
- The determinant is not zero. The determinant of **noninvertible** matrices is zero.
- The inverse of an inverse is the original matrix: $(M^{-1})^{-1}=M$ 
- The inverse of the identity is the identity: $I^{-1}=I$
- The inverse of the transpose is the transpose of the inverse: $(M^T)^{-1}=(M^{-1})^T$
- The inverse of a product is the product of the inverses: $(AB)^{-1}=A^{-1}B^{-1}$
- The determinant of the inverse is the reciprocal of the determinant of the original matrix: $|M^{-1}| = \frac {1}{|M|}$

>The classic way to find out if a matrix is invertible is computing its determinant. If it's not zero, then the matrix is invertible.

There are many ways of computing the inverse of a matrix, although the most common ones are  **classical adjoint** and **gaussian elimination**. 

# Geometric interpretation

The **inverse** of a transformation matrix represents the "opposite transformation", or the transformation that "undoes" the original transformation. So, if we want to apply a transformation and then un-apply it, we can simply:

$$\vec v M M^{-1} = \vec v I = \vec v$$