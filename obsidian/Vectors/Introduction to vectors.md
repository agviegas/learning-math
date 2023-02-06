
Vectors can be defined in two ways:

### Mathematical definition

A **scalar** is a single number. **Vectors** are simply an arrays of numbers. 

>The **dimension** of a vector is the amount of numbers that it contains. Vectors can be of any positive dimension, including 1. In fact, scalars are considered 1D vectors.

There are two types of vectors: **row vectors** and **column vectors**.

$$\vec v =\begin{bmatrix} 1 & 0 & 0 \end{bmatrix} ~~~~~~~~ \vec v= \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}$$
The numbers within a vector can be identified with subscript notation. We could use $\vec v_1$ to talk about the first element of the vector $\vec v$, but in computer graphics is more common to use the letters $x$, $y$, $z$ and $w$ (it's rare to go beyond 4D vectors). So the third element of $\vec v$ is $\vec v_z$.

>The area of mathematics that studies vectors is called **linear algebra**. It uses vectors and matrices of $n$ dimensions are used to solve systems of $n$ linear equations and $n$ unkowns, without caring about about the physical significance of the numbers. This is not of our interests for graphics, where our focus is purely geometric.


### Geometric definition

A vector is a line segment in space. It has 2 properties:

- **Magnitude**: the length of the vector.
- **Direction**: which way the vector is pointing to.

<img width="300px" src="https://mathinsight.org/media/image/image/vector.png" alt="asdf"/>


>**Vectors don't have a fixed position** because they usually describe displacements and relative differences between things. For instance: "The spot that is 3 meters in front of me" could be applied anytime, regardless of my position.

Vectors can be expressed as the coordinates $(x,y,z)$ of the **head** if we move the **tail** to the origin $(0,0,0)$. In other words, the relative displacement from the **tail** to the **head** for each coordinate. When vectors express displacements, we can visualize that the vector $(1,3,-2)$ is a displacement of 1 unit in x, 3 units in y and -2 units in z.

The **zero vector** is any vector where all the components are 0. Is the only vector with a magnitude of 0. This could be understood as the concept of "no displacement". It's the **additive identity** for vectors (adding it to any vector $\vec v$ results in $\vec v$).

___
**Points** are similar to vectors, and mathematically they are the same (an array of numbers / coordinates). Nevertheless, it's important to note the difference in their meaning: points are a place in space, whereas vectors describe a displacement. Two vectors can be added (resulting in a vector) and a point and a vector can be added (resulting in a point), but adding two points doesn't make sense.
___

