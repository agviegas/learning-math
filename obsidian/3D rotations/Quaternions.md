A quaternion expresses a rotation as a scalar $w$ and a 3D vector $v$. It can be expressed in multiple forms. They all mean the same thing. Unlike vectors, there is no distinction between "row" and "column" quaternions. The difference is just aesthetic. 

$$\begin{bmatrix} w & v  \end{bmatrix} ~~~~~~~~~~ \begin{bmatrix} w & \begin{pmatrix} x & y & z  \end{pmatrix}  \end{bmatrix} ~~~~~~~~~~ \begin{bmatrix} w \\ \begin{pmatrix} x \\ y \\ z  \end{pmatrix}  \end{bmatrix}$$


The quaternions, like the [[Axis-angle form and exponential maps|exponential maps]], represent a rotation simply with an angle $\theta$ and an axis $\hat n$. But they aren't stored in the quaternions directly; instead, they are encoded in a way that looks weird but turns out to be very practical:

$$\begin{bmatrix} w & v  \end{bmatrix} = \begin{bmatrix} \cos(\theta/2) & \sin(\theta/2)\hat n  \end{bmatrix}$$
$$\begin{bmatrix} w & \begin{pmatrix} x & y & z  \end{pmatrix}  \end{bmatrix} = \begin{bmatrix} \cos(\theta/2) & \sin(\theta/2)\hat n_x & \sin(\theta/2)\hat n_y & \sin(\theta/2)\hat n_z  \end{bmatrix}$$

So $w$ is related to $\theta$ and $v$ is related to $\hat n$, but they are not the same thing. 

# Negation

There are several operations we can do with quaternions. The most basic one is **negating** a quaternion:
$$-q = \begin{bmatrix} -w & -v  \end{bmatrix} = \begin{bmatrix} -w & \begin{pmatrix} -x & -y & -z  \end{pmatrix}  \end{bmatrix}$$

Surprisingly, this doesn't affect the angular displacement. In other words, the quaternions $q$ and $-q$ describe the same rotation. Thus, each 3D rotation has two distinct representations: $q$ and $-q$.

>This is easy to understand. If we add 360º to $\theta$, the result of the rotation is the same, but all the components of $q$ would be negated. 


# Identity

An **identity quaternion** is a quaternion that doesn't apply any rotation. There are two of them:

$$\begin{bmatrix} 1 & \vec 0  \end{bmatrix} ~~~~~~~~~~ \begin{bmatrix} -1 & \vec 0  \end{bmatrix}$$

- When $\theta$ is an even multiple of 360º, then $cos(\theta)=1$ and we have the first form.
- When $\theta$ is an odd multiple of 360º, then $cos(\theta)=-1$ and we have the second form.
- In both cases $sin(\theta)=0$, so the value of $\hat n$ is irrelevant.

>This makes sense: if $\theta$ is a whole revolution in any axis, the end result is the same as the start, so there is no real change made to the orientation.

Nevertheless, algebraically there's only one true identity quaternion: $\begin{bmatrix} 1 & \vec 0  \end{bmatrix}$. The reason is that the product of any quaternion $q$ by the identity quaternion must result in $q$. If we multiply $q$ by $\begin{bmatrix} -1 & \vec 0  \end{bmatrix}$, the result is $-q$. Above we saw that $q$ and $-q$ represent the same angular displacement, but they are not mathematically the same. This is just a matter of definitions.

# Magnitude

We can compute the magnitude of a quaternion just like we do for [[Vector operations#Magnitude of a vector|vectors]] or imaginary numbers:

$$||q|| = \sqrt{w^2+||v||^2} = \sqrt{w^2+x^2+y^2+z^2}$$
If we substitute by $\theta$ and $\hat n$, we can make an amazing discovery:

$$||q|| = \sqrt{\cos^2(\theta/2)+(\sin(\theta/2)||\hat n||)^2}$$
We know that $\hat n$ is a unit vector, so it's magnitude is always one. Therefore, applying the most basic [[Trigonometry#Trigonometric identities|trigonometric identity]]:

$$||q|| = \sqrt{\cos^2(\theta/2)+\sin^2(\theta/2)} = \sqrt 1 = 1$$

>We only use quaternions to represent orientations, and in this case all quaternions are **normal quaternions** (magnitude = 1).

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

Quaternions can be multiplied. This is sometimes called **Hamilton product**. The result is another quaternion:

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

Knowing the quaternion multiplication and difference we can easily define the difference. The difference between two quaternions $a$ and $b$ is the rotation $d$ that rotates from $a$ to $b$. In other words, the rotation that brings from one orientation to another (remember that quaternion multiplication is from right to left):

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

# Quaternion exponentiation

We can raise quaternions to a scalar power. This is denoted as $q^t$ and shouldn't be confused with the $\exp$ function (which only takes one argument, not 2).

The quaternion exponentiation means the same as for real numbers. For any scalar, $a^0 = 1$ and $a^1 = a$. As the exponent $t$ varies from 0 to 1, $a^t$ varies from 0 to $a$. The same thing happens with quaternion exponentiation: as $t$ varies from 0 to 1, $q^t$ varies from $[1, 0]$ (unit quaternion) to $q$.

Quaternion exponentition is useful because it allows us to get a "fraction" of a rotation. For example, if we wanted to get one third of the rotation $q$, we could simply use $q^{1/3}$.