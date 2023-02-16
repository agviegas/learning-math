
We know that a 3x3 matrix represents a [[Linear transformations|linear transformations]] , so it doesn't contain translation. Fortunately for us, 4x4 matrices allow us to perform a "trick" that allows us to work with translation as another linear transformation.

Let's assume for now that $w=1$. So, any point in 3D space $(x,y,z)$ can be represented in 4D as $(x,y,z,1)$. We can transform 3D transformation matrices into 4D transformation matrices like this:

$$\begin{bmatrix} m_{11} & m_{12} & m_{13} \\ m_{21} & m_{22} & m_{23}  \\ m_{31} & m_{32} & m_{33}  \end{bmatrix} \rightarrow \begin{bmatrix} m_{11} & m_{12} & m_{13} & 0 \\ m_{21} & m_{22} & m_{23} & 0  \\ m_{31} & m_{32} & m_{33} & 0 \\ 0 & 0 & 0 & 1  \end{bmatrix} $$

If we [[Matrix operations#Matrix - vector product|multiply a vector]] $(x,y,z,1)$ by a 4x4 matrix that has this form, we get the same $x,y,z$ result as the 3x3 matrix and $w$ remains as 1. And now we have an additional benefit: due to the matrix algebra rules, now we can express translation as a matrix multiplication.

$$\begin{bmatrix} x & y & z & 1  \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0  \\ 0 & 0 & 1 & 0 \\ \Delta x & \Delta y & \Delta z & 1  \end{bmatrix} = \begin{bmatrix} x + \Delta x & y + \Delta y & z + \Delta z & 1  \end{bmatrix}$$

This matrix multiplication **is an affine transformation** (so it's also **linear**). 4D matrices can't translate points in 4D, and the 4D zero vector will always be transformed back into the 4D zero vector. The reason this works in 3D is that we are [[Linear transformations#Shearing|shearing]] the 4D space, and that results in a translation in 3D. If we check the 3D shearing function in $x,y$, it looks exactly as the translation matrix in 2D:

$$\begin{bmatrix} x & y & 1  \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0  \\ \Delta x & \Delta y & 1  \end{bmatrix} = \begin{bmatrix} x + \Delta x & y + \Delta y & 1  \end{bmatrix}$$

Using this technique, we can use all the [[Linear transformations|linear transformations]] together with translation. The idea is simple: using a 3x3 matrix for 2D and a 4x4 matrix for 3D. We just need to convert these matrices to 3D or 4D respectively like shown above.

>What happens if we apply transformation matrices to a point in infinity $(x,y,0)$ (2D) or $(x,y,z,0)$ (3D)? In that case, all transformations will apply **except for translation**. So we can use $w=0$ to selectively turn off translation, which very convenient for vectors, which [[Introduction to vectors|don't have translation]] (e.g. the normals of a geometry). We can use nutshell: $w=1$ for points and $w=0$ for vectors.

When using 3x3 matrices for 2D or 4x4 matrices for 3D, the right column will always be $(0,0,1)$ or ($0,0,0,1$) respectively. It has no information, but it's convenient to keep it because it is much easier to work with square matrices.

>This technique is not only useful for translating: now we can perform any transformation any pivot point. For instance, imagine that we want to rotate a 3D object around a specific axis. We can simply apply a translation that moves the axis to the origin, apply the rotation, and then unapply the original translation (using its [[Inverse|inverse]]). So the rotation around an arbitrary axis would look like this: $TRT^{-1}$.
