There are a special type of **square matrices** called **orthogonal matrices**. They are very interesting because they are very common in 3D graphics, and computing its [[Inverse|inverse]] is very easy.

# Math interpretation

A square matrix $M$ is orthogonal if and only if the product of the matrix and it's transpose is the identity matrix. That means that it's transpose is it's inverse.

$$MM^T = I \iff M^{-1}=M^T$$

# Geometry interpretation

Orthogonal matrices only contain **rotation** and/or **reflection**. This means that if we know how the matrix has been constructed, we can take advantage of it's orthogonality and save a lot of computations when computing its inverse. 

Let's take a closer look at the definition.

$$kM= \begin{bmatrix} m_{11} & m_{12} & m_{13} \\ m_{21} & m_{22} & m_{23}  \\ m_{31} & m_{32} & m_{33}  \end{bmatrix} \begin{bmatrix} m_{11} & m_{21} & m_{31} \\ m_{12} & m_{22} & m_{32}  \\ m_{13} & m_{23} & m_{33}  \end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0  \\ 0 & 0 & 1  \end{bmatrix}$$

If we develop the matrix product, we get the following nine equations:

$m_{11}m_{11} + m_{12}m_{12} + m_{13}m_{13} = 1$
$m_{11}m_{21} + m_{12}m_{22} + m_{13}m_{23} = 0$
$m_{11}m_{31} + m_{12}m_{32} + m_{13}m_{33} = 0$
$m_{21}m_{11} + m_{22}m_{12} + m_{23}m_{13} = 0$
$m_{21}m_{21} + m_{22}m_{22} + m_{23}m_{23} = 1$
$m_{21}m_{31} + m_{22}m_{32} + m_{23}m_{33} = 0$
$m_{31}m_{11} + m_{32}m_{12} + m_{33}m_{13} = 0$
$m_{31}m_{21} + m_{32}m_{22} + m_{33}m_{23} = 0$
$m_{31}m_{31} + m_{32}m_{32} + m_{33}m_{33} = 1$

Now, interpreting [[Introduction to matrices#Geometric definition|each matrix row as a vector defining a new base]], we can say that:

$$r_1=\begin{bmatrix} m_{11} & m_{12} & m_{13}  \end{bmatrix}$$
$$r_2=\begin{bmatrix} m_{21} & m_{22} & m_{23}  \end{bmatrix}$$
$$r_3=\begin{bmatrix} m_{31} & m_{32} & m_{33}  \end{bmatrix}$$

When we transpose the matrix we are making these vectors the columns. That means that multiplying a row by a column is the same as making the [[Vector operations#Vector dot product|dot product]] between two of them. Now we can make the 9 equations much clearer:

$r_1 \cdot r_1 = 1$               $r_1 \cdot r_2 = 0$               $r_1 \cdot r_3 = 0$
$r_2 \cdot r_1 = 0$               $r_2 \cdot r_2 = 1$               $r_2 \cdot r_3 = 0$
$r_3 \cdot r_1 = 0$               $r_3 \cdot r_2 = 0$               $r_3 \cdot r_3 = 1$

This gives us very valuable information:

>If the dot product of a vector with itself is 1, it means that it's a **unit vector**. That means that $r_1$, $r_2$ and $r3$ are unit vectors.

>The dot product of two vectors is zero only if they are **perpendicular**. So $r_1$, $r_2$ and $r_3$ are perpendicular to each other.

>The first two statments mean that the 3 vectors form an **orthonormal basis**.

>3 of the 9 equations above are redundant because the dot product is commutative. That means that these equations express only 6 constraints, leaving out 3 degrees of freedom.

>This also applies for the columns of the matrix. So if $M$ is orthogonal, $M^T$ is orthogonal.

If we don't know in advance if the matrix is orthogonal, we won't take advantage of this, because checking it would be a waste of time (checking orthogonality + transposing would take the same time as just [[Inverse|inverting]] it).

___
Beware: matrices that are orthogonal in the abstract may not be exactly orthogonal when represented in floating point, so we have to use tolerances that have to be tuned.
___

# Orthogonalizing a matrix

Sometimes we find a matrix that is slightly out of orthogonality. Maybe because we got bad data from an external source, or because we accumulated floating point error (which is called **matrix creep**). For instance, for basis vectors used for **bump mapping** we will often adjust the basis to be orthogonal, even if the texture mapping gradients aren't quite perpendicular.

In these cases we want to **orthogonalize** the matrix, resulting in a matrix that is orthogonal and is (hopefully) close enough to the original matrix. The basic algorithm for doing this is the **Gram-Schmidt orthogonalization**. The idea is to go through the basis vectors in order: for each one, we subtract off the portion that is parallel to the proceeding vectors, thus resulting in a perpendicular vector.

For instance, given a 3x3 matrix, we can orthogonalize it like this:

$$r'_1=r_1$$
$$r'_2=r_2 - \frac {r_2-r'_1}{r'_1 \cdot r'_1}r'_1$$
$$r'_3=r_3 - \frac {r_3-r'_1}{r'_1 \cdot r'_1}r'_1- \frac {r_3-r'_2}{r'_2 \cdot r'_2}r'_2$$

After this, the three new vectors are guaranteed to be **perpendicular** (**orthogonal**), but not necessarily **unit**. We need an **orthonormal basis**, so we need to [[Vector operations#Vector normalization|normalize]] the vectors. Two things to keep in mind about this algorithm:

- Only in 3D, we could compute the third vectoras a cross product of the first two: $r'_3 = r'_1 \times r'_2$

- It is dimensionally biased, because $r_1$ doesn't change and $r'_3$ changes a lot. A way of avoiding this is to only subtract a fraction $k$ of the projection, and not all of it, from the original basis, and not the transformed one. The algorithm looks like this:

$$r'_1=r_1 - k\frac {r_1\cdot r_2}{r_2 \cdot r_2}r_2 - k\frac {r_1\cdot r_3}{r_3 \cdot r_3}r_3$$
$$r'_2=r_2 - k\frac {r_2\cdot r_1}{r_1 \cdot r_1}r_1 - k\frac {r_2\cdot r_3}{r_3 \cdot r_3}r_3$$
$$r'_3=r_3 - k\frac {r_3\cdot r_2}{r_2 \cdot r_2}r_2 - k\frac {r_3\cdot r_1}{r_1 \cdot r_1}r_1$$

One iteration of this algorithm results in a basis of 3 vectors that is slightly more orthogonal than the original one, but probably not completely orthogonal. We can repeat this procedure many times (for instance, $k=\frac 1 4$ and execute this 10 times), we can approximate the basis to a orthogonal base a lot. Then, finally, we can apply the original Gram-Schmidt algorithm to get a real orthogonal base, and the bias will be very very small (because the base is already very close to being orthogonal).

