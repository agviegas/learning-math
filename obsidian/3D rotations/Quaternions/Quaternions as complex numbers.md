We need to build some parallels between complex numbers and matrices to understand this.

Let's start simple and imagine that we want to represent the set of real numbers as 2x2 matrices. If $a$ is any real number, the easiest way would be to do this:

$$ \begin{bmatrix} a & 0 \\ 0 & a \end{bmatrix}$$

This is very convenient because it preserves the algebra rules of addition, subtraction and multiplication (associative property, distributive property, etc). For instance:

$$ \begin{bmatrix} a & 0 \\ 0 & a \end{bmatrix} + \begin{bmatrix} b & 0 \\ 0 & b \end{bmatrix} = \begin{bmatrix} a+b & 0 \\ 0 & a+b \end{bmatrix}$$

Now, if we wanted to do the same for [[Arithmetic operations#Complex numbers|complex numbers]], it's really simple. Before, we had one degree of freedom. Now we have 2, $a$ and $b$. It looks like this:

$$a +bi \equiv \begin{bmatrix} a & -b \\ b & a \end{bmatrix}$$
This matrix behaves like normal complex numbers. For instance:

$$\begin{bmatrix} a & -b \\ b & a \end{bmatrix} + \begin{bmatrix} c & -d \\ d & c \end{bmatrix} = \begin{bmatrix} a+c & -(b+d) \\ b+d & a+c \end{bmatrix}$$

Even the equation $i^2=-1$ is true with this:

$$\begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}^2 = \begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}\begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix} = \begin{bmatrix} -1 & 0 \\ 0 & -1 \end{bmatrix}$$

If we interpret the columns of this matrix as a [[Introduction to matrices#Geometric definition|basis vector system]], we would be converting the vectors $[0,1]$ and $[-1, 0]$ into $[-1, 0]$ and $[0, -1]$. In other words, we can interpret multiplying by $i$ as applying a 90º rotation. In fact, $i^2$  would be a 180º rotation, and thus the result -1 makes sense.

>We shouldn't think of complex numbers $a + bi$ as something mystical. It's just a number with two degrees of freedom, or two parts that are "orthogonal" to each other.

This means that we can represent any rotation $\theta$ using this schema. In fact, this is just the [[Linear transformations#Rotation|same matrix that we use for 2D rotation]] (although here it's transposed, because we will operate with column vectors later).

$$\cos \theta + i \sin \theta = \begin{bmatrix} cos(\theta) & -sin(\theta) \\ sin(\theta) &  cos(\theta)\end{bmatrix}$$

Notice how complex conjugation (negating the complex part) corresponds to matrix transposition. The same way as the conjugate of a quaternion expresses the opposite rotation, the transpose of a rotation matrix (which is [[Orthogonal matrices|orthogonal]]) expresses the opposite rotation.

This parallelism between complex numbers and matrix transformations also applies to vectors. We can interpret a vector $[x,y]$ as the complex number $[x+iy]$, and then we can interpret the multiplication of two complex numbers as performing a rotation:

This is how it looks for complex numbers:

$$(\cos \theta + i \sin \theta)(x+iy) = (x \cos \theta - y \sin \theta) + i(x \sin \theta + y \cos \theta)$$

And this is how it looks for matrices:

$$ \begin{bmatrix} \cos \theta & -\sin\theta \\ \sin \theta &  \cos\theta\end{bmatrix} \begin{bmatrix} x  \\ y \end{bmatrix} = \begin{bmatrix} x \cos \theta - y \sin \theta  \\ x \sin \theta + y \cos \theta \end{bmatrix}$$

This parallels look like nothing more than a math trivia, but they will be useful in a moment. In order to use complex numbers in 3D we need more dimensions, and it turns out that the only way to do this is to use numbers with 1 real part and 3 imaginary parts. They were invented by William Hamilton in the XIX century and were called **quaternions**. They have three imaginary parts $i$, $j$, $k$ and follow the **Hamilton rules**:

$$i^2=j^2=k^2=-1$$
$$ij=k ~~~~~~ ji = -k$$
$$jk=i ~~~~~~ kj = -i$$
$$ki=j ~~~~~~ ik = -j$$

So the quaternion notation $[w, (x, y, z)]$ corresponds to the complex number $w + xi + yj + zk$. The definition of [[Quaternions basic operations#Multiplication||quaternion multiplication]] are derived from this. We can now translate this to 4x4 matrices, where any real number $a$ is mapped to the following matrix:

$$a \equiv \begin{bmatrix} a & 0 & 0 & 0 \\ 0 & a & 0 & 0 \\ 0 & 0 & a & 0 \\ 0 & 0 & 0 & a  \end{bmatrix}$$

And the complex numbers $i$, $j$ $k$ are mapped to the matrices. This form follow the **Hamilton equations**.

$$i \equiv \begin{bmatrix} 0 & 0 & 0 & 1 \\ 0 & 0 & -1 & 0 \\ 0 & 1 & 0 & 0 \\ -1 & 0 & 0 & 0  \end{bmatrix} ~~~~~ j \equiv \begin{bmatrix} 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \\ -1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0  \end{bmatrix} ~~~~~ k \equiv \begin{bmatrix} 0 & -1 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & -1 & 0  \end{bmatrix}$$

Combining all the above parallels and associations, we can convert any quaternion to a transformation matrix like this:

$$w+xi+yj+zk = \begin{bmatrix} w & -z & y & x \\ z & w & -x & y \\ -y & x & w & z \\ -x & -y & -z & w  \end{bmatrix}$$

>Again, we observe that complex conjugation (negating $x$, $y$ and $z$) corresponds to matrix transposition.

Now, let's get back to quaternions as rotations. It's noticeable that the upper left part of the $k$ matrix is exactly the same as the 2D rotation matrix explained above. This indicates that a part of $k$ is a 90º rotation about the $z$ axis. 

Doing the same as we did for 2D, we might expect that we can represent any rotation in the $z$ axis as $\cos \theta + k \sin \theta$. Let's try this by rotating something. Given the simple unit vector in the $x$ axis $[1, 0, 0]$, let's rotate it around the $k$ axis. To do this, we must represent the vector in its complex form, which is $0 + 1i + 0j + 0k$, so it's just $i$:

$$(\cos \theta + k \sin \theta)i = i \cos \theta + ki \sin \theta = i \cos \theta + j \sin \theta$$

And this corresponds to $[\cos \theta, \sin \theta, 0]$ , which is exactly what we would expect. So this worked! But now let's try it with a more general vector $[1, 0, 1]$ (whose complex form is $i + k$):

$$(\cos \theta + k \sin \theta)(i+k) = i \cos \theta + j \sin \theta + k\cos \theta - \sin \theta$$

Unfortunately, the result doesn't correspond to a 3D vector because $w$ has a nonzero value. If we convert this to a 4x4 matrix form, we'll see that this contains a rotation in the $zw$ hyperplane:

$$\cos \theta + k \sin \theta \equiv \begin{bmatrix} \cos\theta & -\sin\theta & 0 & 1 \\ \sin\theta & \cos\theta & 0 & 0 \\ 0 & 0 & \cos\theta & \sin \theta \\ 0 & 0 & -\sin \theta & \cos\theta  \end{bmatrix} $$

The upper top left half of the matrix is what we want; the bottom right part is not wanted and produces wrong results for rotations. We can get rid of this by using a nice trick. First, we invert the order of multiplication. This has the effect of inverting the $y$ coordinate, so now we have a rotation by $-\theta$. So we also need make a negative rotation, which is just using the conjugate of the quaternion (negating the imaginary part):

$$(i+k)(\cos \theta - k \sin \theta) = i \cos \theta + j \sin \theta - k\cos \theta + \sin \theta$$

>So multipliying on the right gives us the rotation we want, plus an undesired rotation. Multiplying on the left by the conjugate also gives us the rotation we want, plus the negative of that same undesired rotation. So if we combine both operations, we get rid of the undesired part and we get the correct rotation, with just one problem left: we are applying the rotation twice. This is the reason behind the $\theta / 2$ of the quaternion equations.

