
# Matrix transposition

The transpose of a matrix $M$ of dimension $ij$ is a matrix $M^T$ of dimension $ji$ where the columns and rows have been flipped. 

$$M^T= \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6  \\ 7 & 8 & 9  \end{bmatrix}^T = \begin{bmatrix} 1 & 4 & 6 \\ 2 & 5 & 8  \\ 3 & 5 & 9  \end{bmatrix} $$ 
- Transposing a **row vector** results in a **column vector** and viceversa.
- For any matrix: $(M^T)^T = M$
- For any diagonal matrix: $D^T = D$

# Matrix - scalar product

The product of a matrix $M$ and a scalar $k$ results in a matrix of the same dimension where all elements have been multiplied by $k$.

$$kM= k\begin{bmatrix} m_{11} & m_{12} & m_{13} \\ m_{21} & m_{22} & m_{23}  \\ m_{31} & m_{32} & m_{33}  \end{bmatrix} = \begin{bmatrix} km_{11} & km_{12} & km_{13} \\ km_{21} & km_{22} & km_{23}  \\ km_{31} & km_{32} & km_{33}  \end{bmatrix}$$

# Matrix - matrix product

Two matrices $A_{ij}$ and $B_{jk}$ can be multiplied only if the **number of columns** of $A$ is equal to the **number of rows** of $B$. It results in a new matrix of dimension $ik$.

$$A_{ij} ~ B_{jk} = C_{ik} $$
Each element of the resulting matrix is computed using the following formula:

$$ c_{ij} = \sum^n_{k=1}a_{ik} b_{kj} $$
It looks complicated, but the pattern is quite simple. For example:

$$AB= \begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix} \begin{bmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{bmatrix} = \begin{bmatrix} a_{11}b_{11} + a_{12}b_{21} & a_{11}b_{12} + a_{12}b_{22} \\ a_{21}b_{11} + a_{22}b_{21} & a_{21}b_{12} + a_{22}b_{22} \end{bmatrix}$$

- Multiplying two square matrices result in a square matrix of the same dimension.

- Multiplying any matrix by the identity matrix $I$ has no effect (it's the **product identity**).

- Matrix multiplication is **not conmutative**: $AB \neq BA$

- Matrix multiplication is **associative**: $(AB)C = A(BC)$.

- Matrix multiplication is **associative** even with scalars:  $k(AB) = (kA)B = A(kB)$.

- Matrix multiplication is **distributive** over vector addition: $(v+w)M = vM + wM$

- The transpose of a product is the product of the tranpose in reverse order: $(AB)^T=B^TA^T$

# Matrix - vector product

Multiplying a [[Introduction to vectors|vector]] and a matrix is the same as the matrix-matrix product if we consider vectors as 1 dimensional matrices. Because of the dimensional restrictions, here are all the possible scenarios. This works the same regardless of the number of dimensions of the vector - matrix (within the dimensional restrictions).

___
**Row vector left**

$$\vec rA= \begin{bmatrix} x & y & z  \end{bmatrix} \begin{bmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{bmatrix} $$
$$\vec rA= \begin{bmatrix} x~a_{11} +y~a_{21} + z~a_{31} & x~a_{12} + y~a_{22} +z~a_{32} & x~a_{13} + y~a_{23} +z~a_{33}  \end{bmatrix}$$
---
**Row vector right**
$$A\vec r= undefined $$
___
**Column vector left**

$$\vec c A= undefined $$
___
**Column vector right**

$$A \vec c= \begin{bmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} x~a_{11} + y ~ a_{12} + z ~a_{13} \\ x~a_{21} + y ~ a_{22} + z ~a_{23} \\ x~a_{31} + y ~ a_{32} + z ~a_{33} \end{bmatrix}  $$
___

Ignoring the fact that one result is a **row vector** and the other is a **column vector**, we can see that the components of the results are different. If we want consistent results, we will need to transpose the matrix in the **column vector** case). 

This makes sense, because in the end, the **column vector** is the transpose of the **row vector**, and $AB^T \neq AB$. If we transpose the matrix before the multiplication, we'll get $A^TB^T=(AB)^T$, which is the transpose of the result we get with **row vectors** ($AB$). 

>For **row vectors**, sequence of transformation matrices are applied from left to right ($\vec v ABC$) while in **column vectors** the transformation sequence needs to be from right to left ($CBA\vec v$). 

Whenever we are using a graphics API or reading a book or documentation, we should keep this in mind, as some of them use **row vectors** and others use **column vectors**. For instance, **DirectX** and **WebGL** use **row vectors**, while **openGL** (and almost any scientific publication) use **column vectors**. 

___
Other interesting facts about the vector-matrix operation:

- Each element in the resulting vector is the dot product between the vector and the respective row or column of the matrix.

- The resulting vector is always a **linear combination** of the rows or columns of the matrix.
___
