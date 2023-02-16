For square matrices there is a special scalar named **determinant** of the matrix. It has very useful properties in linear algrebra and geometric interpretations.

# Math interpretation

The determinant of a matrix $M$ is denoted as $|M|$ or $\det M$. The determinant of a 2x2 matrix looks like this:

$$|M| = \left | \begin{array}. m_{11} & m_{12} \\ m_{21} &  m_{22}\end{array} \right | = m_{11}m_{22}-m_{12}m_{21} $$

So we are just multiplying the diagonals, and subtracting the second diagonal to the first one. The determinant of a 3x3 matrix is significantly more convoluted:

$$|M| = \left | \begin{array}. m_{11} & m_{12} & m_{13} \\ m_{21} &  m_{22} & m_{23} \\ m_{31} &  m_{32} & m_{33} \end{array} \right | $$
$$|M| = m_{11}m_{22}m_{33} + m_{12}m_{23}m_{31} + m_{13}m_{21}m_{32}
− m_{13}m_{22}m_{31} − m_{12}m_{21}m_{33} − m_{11}m_{23}m_{32} $$


<img width="300px" src="https://www.algebrapracticeproblems.com/wp-content/uploads/2021/02/rule-of-sarrus.png?ezimgfmt=rs:240x177/rscb1/ngcb1/notWebP" alt="asdf"/>

There's an easier way of remembering this. If we consider the 3 rows of a 3x3 matrix as basis vectors, the determinant is the **triple product** between them:

$$|M| = \left | \begin{array}. a_x & a_y & a_z \\ b_x & b_y & b_z \\ c_x & c_y & c_z \end{array} \right | = (a \times b) \cdot c$$

The computation of the determinant for bigger matrices becomes very complex, and of course it's pointless to try to memorize it. But we should know some important properties about determinants:

- The determinant of the identity matrix is one: $|I| = 1$
- The determinant of a product is equal to the product of determinants: $|AB|=|A||B|$
- A matrix and its transpose have the same determinant: $|M|=|M^T|$
- If any row or column in a matrix is all 0s, the determinant is 0.
- Exchanging any pair of rows or columns negates the determinant.


# Geometric interpretation

The determinant of a matrix has very interesting geometric interpretations. In 2D, it's equal to the the **signed area** of the parallelogram that has the [[Introduction to matrices|basis vectors (rows of the matrix)]] as two sides. The area is "signed" because it can be negative if the shape is "flipped".

<img width="300px" src="
https://upload.wikimedia.org/wikipedia/commons/thumb/a/ad/Area_parallellogram_as_determinant.svg/220px-Area_parallellogram_as_determinant.svg.png" alt="asdf"/>
Similarly, in 3D the determinant is the volume of the parallelepiped formed by the 3 basis vectors (rows of the matrix). It will be negative if the volume is "turned inside out". The determinant will give us interesting information about the transformation:

>The determinant is related to the change in area (in 2D) or volume (in 3D) that will occur as a result of transforming an object by the matrix. 

>If the determinant of the matrix is 0, the matrix contains a **projection**. This makes sense, because it means that one of the rows of the matrix is not linearly independent, so it's not a new dimension. In other words, it's like saying the matrix only has 2 dimensions, and that is what a projection does.

>If the determinant of the matrix is negative, there is a reflection inside the matrix (which is the only operation that "turns the object inside out").

