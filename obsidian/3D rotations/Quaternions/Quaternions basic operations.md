# Conjugate and inverse

The **conjugate** of a quaternion $q$ is denoted as $q^*$ and is the result of negating $v$. This has to do with the interpretation of the quaternion as a complex number, explained far below.

$$q^* = \begin{bmatrix} w & -v  \end{bmatrix} = \begin{bmatrix} w & \begin{pmatrix} -x & -y & -z  \end{pmatrix}  \end{bmatrix}$$

The **inverse** of a quaternion $q$ is denoted as $q^{-1}$ and is defined as its conjugate divided by its magnitude. We have to keep in mind that when we use quaternions for rotations, the magnitude is always one, so **for our use case, the conjugate of a quaternion is its inverse**.
$$q^{-1} = \frac {q^*}{||q||}$$
Similarly to scalars, the product of a quaternion by its inverse equals the identity:

$$q^{-1} q = q ~q^{-1} = \begin{bmatrix} 1 & \vec 0  \end{bmatrix} $$

>The **inverse quaternion** represents the opposite rotation. We can apply a rotation $q$, and then unapply it as $q^{-1}$. It's very easy to see this when we think in the inverse as the conjugate. We are simply negating the axis of rotation $\hat n$, whereas the angle $\theta$ doesn't change. That means that we are performing the same rotation, but in the opposite direction. 

___
For our purposes, we could have also defined the conjugate as negating $\theta$ and leaving $v$ unchanged, but the term _conjugate_ has a specific meaning in imaginary numbers. We will explain this further below.
___

# Multiplication

Quaternions can be multiplied. Multiplying a quaternion A by another B means **applying the rotation of A to B**. This is sometimes called Hamilton product. The result is another quaternion that contains the resulting rotation.

$$q_1~q_2 = \begin{bmatrix} w_1 & \begin{pmatrix} x_1 & y_1 & z_1  \end{pmatrix}  \end{bmatrix} \begin{bmatrix} w_2 & \begin{pmatrix} x_2 & y_2 & z_2  \end{pmatrix}  \end{bmatrix}$$
$$=\begin{bmatrix} w_1w_2 - x_1x_2 - y_1y_2 - z_1z_2 \\ \begin{pmatrix} w_1x_2 + x_1w_2 + y_1z_2 - z_1y_2 \\ w_1y_2 + y_1w_2 + z_1x_2 - x_1z_2 \\ w_1z_2 + z_1w_2 + x_1y_2 - y_1x_2  \end{pmatrix}  \end{bmatrix}$$
$$=\begin{bmatrix} w_1 & v_1  \end{bmatrix}\begin{bmatrix} w_2 & v_2  \end{bmatrix} = \begin{bmatrix} w_1w_2 - v_1 \cdot v_2 & w_1v_2 + w_2v_1 + v_1 \times v_2  \end{bmatrix}$$

- It's associative: $(ab)c = a(bc)$
- It's not conmutative: $ab \neq ba$
- The magnitude of the product equals the product of the magnitudes. This is important because it means that if we multiply two unit quaternions, the result is a unit quaternion: $||ab|| = ||a|| ~~ ||b||$

Another interesting property of multiplication is that we can easily rotate any point or vector with a weird trick. Let's imagine the point $(x,y,z)$. We can "expressed it like a quaternion" like this: $p=[0, (x,y,z)]$. This is not a valid rotation quaternion because it can have a magnitude, but let's ignore that. Now, we can apply a rotation quaternion $q$ to that point (resulting in another point $p'$) like this:

$$p' = q~p~q^{-1}$$

Although this is a nice trick that could be use to rotate vectors or points, the computation is actually the same as converting the quaternion to a [[Linear transformations|rotation matrix]], so it's not very common to use this. Nevertheless, this has very important (and practical) consequences. Imagine that we apply a rotation $a$ and then a rotation $b$ to a point. It would look like this:

$$p' = b(a~p~a^{-1})b^{-1} = (ba)p(ba)^-1 $$

>So applying a rotation $a$ and then a rotation $b$ is the same as applying the single rotation $ba$. This  means that quaternion multiplication can be used to concatenate multiple rotations, just like matrix multiplication. Nevertheless, for quaternions the order of multiplication is always inverse to the order of rotations applied (if we want to apply $a$ and then $b$, we need to compute the product $ba$).


# Difference

Knowing the quaternion multiplication and inverse we can easily define the difference. The difference between two quaternions $a$ and $b$ is the rotation $d$ that rotates from $a$ to $b$. In other words, the rotation that brings from one orientation to another (remember that quaternion multiplication is from right to left):

$$da = b$$
$$d = ba^{-1}$$
Now we have a super easy way to go from one rotation to another, which is very useful for interpolations and animations.


# Dot product

Quaternions have a dot product operation defined and, just like [[Vector operations#Vector dot product|vector dot product]], the result is a scalar and, if the quaternions are unit quaternions, is contained between 1 and -1.

$$q_1 \cdot q_2 = \begin{bmatrix} w_1 & v_1  \end{bmatrix} \cdot \begin{bmatrix} w_2 & v_2  \end{bmatrix} = w_1w_2 + v_1 \cdot v_2 = w_1w_2 + $$
$$= w_1w_2 + x_1x_2 + y_1y_2 + z_1z_2$$

This operation is not very common in 3D programming, but it has interesting geometric meaning. For instance, in the [[#Difference|difference]], the $w$ of the result is $a \cdot b$. That means that $a \cdot b = cos(\theta / 2)$, with $\theta$ being the angle needed to go from $a$ to $b$. So it has a similar interpretation to the [[Vector operations#Vector dot product|vector dot product]]: the greater the result, the more "alike" the orientations are (as if they are the same, $\theta = 0$ and $cos(0/2) = 1$). 

For measuring the similarity between two quaternions we are usually interested only in the absolute value of $a \cdot b$, since $a \cdot b = -(a \cdot (-b))$, even though $b$ and $-b$ represent the same angular displacement. So we can compare the "alikness" $a$ of two quaternions like this (with $|~|$ being the absolute function):

$$a =|q_1 \cdot q_2|$$

The dot product is also useful for computing the **slerp** function.

# Log, exp and scalar multiplication

These three operations are not usually used directly but are the basis for several important quaternion operations. First, if we define $\alpha=\theta / 2$, we can reformulate quaternions like this:

$$\begin{bmatrix} w & v  \end{bmatrix} = \begin{bmatrix} \cos(\alpha) & \sin(\alpha)\hat n  \end{bmatrix}$$

The **logarithm** function is defined like this:

$$\log q = \log(\begin{bmatrix} \cos(\alpha) & \sin(\alpha)\hat n  \end{bmatrix} \equiv \begin{bmatrix} 0 & \alpha\hat n  \end{bmatrix}$$

The symbol $\equiv$ means "equal by definition". In general, $\log q$ is **not a unit quaternion**. It's interesting to see the similarity between the log of a quaternion and the [[Axis-angle form and exponential maps|exponential map form]].

The exponential function is exactly the opposite. First we define a quaternion $p$ to have the form $\begin{bmatrix} 0 & \alpha\hat n  \end{bmatrix}$. This function **always returns a unit quaternion**.

$$\exp q = \exp\begin{bmatrix} 0 & \alpha\hat n  \end{bmatrix} \equiv (\begin{bmatrix} \cos(\alpha) & \sin(\alpha)\hat n  \end{bmatrix} $$

Just like with scalars, exponent and logarithm operations are inverses of each other.

$$\exp(\log(q)) = q$$

Quaternions can also be multiplied by a scalar like this. This usually doesn't result in a unit quaternion, so this operation is not useful for using quaternions for rotations.

$$k~q = k\begin{bmatrix} w & v  \end{bmatrix}  = \begin{bmatrix} kw & kv  \end{bmatrix} $$
