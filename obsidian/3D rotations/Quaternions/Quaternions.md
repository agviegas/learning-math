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

