
Matrices can be defined in 2 ways:

### Mathematical definition

A matrix is a rectangular grid of numbers. It has **rows** and **columns**. While a [[Introduction to vectors|vector]] is an array of **scalars**, a matrix is an array of **vectors**.

>The **dimension** of a matrix is the number of rows and columns that it contains. For example, a 3x4 matrix has 3 rows and 4 columns. 

$$I= \begin{bmatrix} 1 & -3 & 8 & 14 \\ \sqrt 2 & 1 & 3 & -7 \\ 0 & -9 & 3 & \frac 53  \end{bmatrix}$$

Matrix are represented with an uppercase letter. The numbers within a matrix can be identified with the corresponding lowercase letter and subscript notation indicating the **row** and the **column**. For instance, $i_{21}$ is the element in the second row and the first column of the matrix $I$ (which in this example is $\sqrt 2$).

>Matrices in programming are represented as a single-dimension array that lists the elements of each row for each column. For instance, a 4x4 matrix would be a 16-number array.

- A **square matrix** is a matrix with the same number of rows and columns. 3D math is mainly focused in 2x2, 3x3 and 4x4 matrices. 

- A **diagonal matrix** is a **square matrix** where only the **diagonal elements** are not zero.

- An **identity matrix** is a **diagonal matrix** where all the **diagonal elements** are 1. Their dimension can be denoted with subscript notation.

$$I_4= \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1  \end{bmatrix}$$
>[[Introduction to vectors|Vectors]] can be seen as a 1-D matrix. A vector of $n$ dimensions can be either a 1 x $n$ matrix (**row vector**) or as a $n$ x 1 matrix (**column vector**). This distinction will have a huge impact when making operations between vectors and matrices.

### Geometric definition

Matrices in 3D math are used primarily to define the relationship between 2 coordinate spaces. In simpler words, they represent a **[[Linear transformations|linear transformation]] of a coordinate space**.

It's important to _see_ what a transformation matrix really means in order to understand how it works. An easy way to do this is to [[Matrix operations#Matrix - vector product|multiply]] the **standard basis vectors** $i$, $j$ and $k$ by an arbitrary matrix $M$:

$$iM = \begin{bmatrix} 1 & 0 & 0  \end{bmatrix} \begin{bmatrix} m_{11} & m_{12} & m_{13} \\ m_{21} & m_{22} & m_{23} \\ m_{31} & m_{32} & m_{33} \end{bmatrix} = \begin{bmatrix} m_{11} & m_{12} & m_{13}  \end{bmatrix}$$
$$jM = \begin{bmatrix} 0 & 1 & 0  \end{bmatrix} \begin{bmatrix} m_{11} & m_{12} & m_{13} \\ m_{21} & m_{22} & m_{23} \\ m_{31} & m_{32} & m_{33} \end{bmatrix} = \begin{bmatrix} m_{21} & m_{22} & m_{23}  \end{bmatrix}$$
$$kM = \begin{bmatrix} 0 & 0 & 1  \end{bmatrix} \begin{bmatrix} m_{11} & m_{12} & m_{13} \\ m_{21} & m_{22} & m_{23} \\ m_{31} & m_{32} & m_{33} \end{bmatrix} = \begin{bmatrix} m_{31} & m_{32} & m_{33}  \end{bmatrix}$$

>Each row in the matrix contains the result of performing the transformation in that dimension. **Each row of the matrix is a basis vector that defines the new $i$, $j$ and $k$ respectively, forming a new coordinate system**. 

We know that any vector can be expressed as a linear combination of the **basis vectors**:

$$\vec v = v_xi+v_yj+v_zk$$

Substituting above, we can now bring any vector to that new coordinate system, also known as **applying the transformation on that vector**:

$$\vec vM = v_x\begin{bmatrix} m_{11} & m_{12} & m_{13}  \end{bmatrix}+v_y\begin{bmatrix} m_{21} & m_{22} & m_{23}  \end{bmatrix}+v_z\begin{bmatrix} m_{31} & m_{32} & m_{33}  \end{bmatrix}$$

Let's see this in practice. Let's consider the following matrix M:

$$M= \begin{bmatrix} 2 & 1 \\ -1 & 2 \end{bmatrix}$$

What transformation does this matrix represent? Knowing that each row represents the basis vector for that dimension, we can see that $p=\begin{bmatrix} 2 & 1 \end{bmatrix}$  and $q=\begin{bmatrix} -1 & 2 \end{bmatrix}$. In other words, we are creating a new **coordinate system** $p$, $q$ that looks like this:

![[Pasted image 20230209173549.png]]

Now we can map any point from $i$,$j$ to the new coordinate system $p,q$ simply by multiplying by $M$.

![[Pasted image 20230209174420.png]]

This is a very powerful tool for two reasons: 

- It allows us to easily visualize the transformation that a matrix performs (or, in other words, the **new coordinate system that it defines**).

- It allows us to create new matrices that define transformations! All we need to know is how it transforms the basis vectors. 

### Linear algebra applications

Matrices are used in **linear algebra** to solve system of ecuations, which can be useful in more advanced use cases: fluid, cloth, and hair simulations (and rendering); more robust procedural animation of characters; real-time global illumination; machine vision; gesture recognition; etc.