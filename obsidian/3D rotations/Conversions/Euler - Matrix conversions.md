# Euler to matrix

[[Euler angles]] define a sequence of three simple rotations around the axis. So converting from Euler to matrix is as simple as creating the 3 [[Linear transformations#Rotation|basic rotations as matrices]] and concatenate them into a single matrix. 

The caveat is that if we apply Euler angles normally, the rotations are applied in the **local space**, so that each rotation affects the next one. To prevent this, we can just use [[Euler angles|fixed axes]] by  doing the rotations in the reverse order: instead of **heading, pitch, bank**, we will do **bank, pitch, heading**.

$$B =R_z(b)= \begin{bmatrix}\cos b & \sin b & 0 \\ -\sin b & \cos b & 0 \\ 0 & 0 &  1 \end{bmatrix}$$
$$P = R_x(p) = \begin{bmatrix}1 & 0 & 0 \\0 & \cos p & \sin p \\ 0 & -\sin p &  \cos p \end{bmatrix}$$
$$H= R_y(h) \begin{bmatrix}\cos h & 0 & -\sin h \\0 & 1 & 0 \\ \sin h & 0 &  \cos h\end{bmatrix}$$
$$BPH = $$
$$\begin{bmatrix}\cos h \cos b + \sin h \sin p \sin b & \sin b \cos p & -\sin h \cos b + \cos h \sin p \sin b \\- \cos h \sin b + \sin h \sin p \cos b & \cos b \cos p & \sin b \sin h + \cos h \sin p\cos b \\ \sin h \cos p & -\sin p &  \cos h \cos p\end{bmatrix}$$


# Matrix to Euler

This technique for converting matrix rotations to Euler angles use 2 assumptions as starting point:

>Since there are infinite Euler angles that represent a given angular displacement due to [[Euler angles#Aliasing|aliasing]], we will use a technique that always returns the **canonical** Euler angles.

>This technique assumes that the matrices that we use as input don't have a big accumulated precission error (so they are at least almost orthogonal). Also, they must contain only rotation (not other concatenated transformations).

Using the $BPH$ matrix as starting point, we can solve for $p$ immediately using $m_{32}$:

$$m_{32}=-\sin p$$
$$p = -\arcsin(-m_{32})  $$
>Usually, math libraries have an `asin()` function that returns a value in the range of $[-90º, +90º]$, which is exactly what we need for the pitch of our **canonical form** of Euler angles.

Let's assume that the pitch is neither 90º nor -90º, which means that $\cos p \neq 0$. We can determine $\sin h$ and $\cos h$ by dividing $m_{13}$ and $m_{33}$:

$$m_{31} = \sin h \cos p \rightarrow \sin h = \frac {m_{31}}{\cos p}$$
$$m_{33} = \cos h \cos p \rightarrow \cos h = \frac {m_{33}}{\cos p}$$
Now that we know the sine and cosine of $h$, we can determine the angle using the **atan2** function, which returns an angle in the range $[180º, -180º]$, which is again our desired range for the heading in the **canonical form** of the Euler angles.

>Remember: just knowing the sine or cosine is not enough to uniquely identify an angle outside of the range $[-90º, +90º]$, so we can't use the formulas $arccos$ or $arcsin$ directly.

$$h = atan2(\sin h, \cos h) = atan2(\frac {m_{31}}{\cos p}, \frac {m_{33}}{\cos p})$$

However, we can simply this knowing that `atan2` works by taking the arctangent of the quotient x/y and using the signs of the two arguments to place the result in the correct quadrant. So multiplying both arguments by the same number should not change the result. Therefore, if we multiply both arguments by $\cos p$:

$$h=atan2(m_{31}, m_{33})$$
Bank is computed similarly for $m_{12}$ and $m_{22}$:

$$m_{12} = \sin b \cos p \rightarrow \sin b=\frac{m_{12}}{\cos p}$$
$$m_{22} = \cos b \cos p \rightarrow \cos b=\frac{m_{22}}{\cos p}$$
$$b = atan2(m_{12}, m_{22})$$

Of course, we can't use this operations if $p=90º$ or $p=-90º$ because then $\cos p=0$ and we would be dividing by zero. But notice that when this happens, we are either looking straight up or straight down, and this is a **Gimbal lock** situation, where heading and bank rotate around the same horizontal plane. 

As we know, this has infinite solutions, so we will arbitrarily assign all the rotation to the heading and assume that the bank is zero ($b=0$), and we just need to solve for the heading. Assuming that:

$$\cos p = 0 ~~~~ b=0 ~~~~ \sin b = 0 ~~~~ \cos b = 1$$
If we apply this to the general equation that we got at the end of the [[#Euler to matrix#euler to matrix transformation]], we get the following:

$$\begin{bmatrix}\cos h & 0 & -\sin h \\\sin h \sin p & 0 & \cos h \sin p \\ 0 & -\sin p &  0\end{bmatrix}$$

And we can simply compute the heading $h$ from $-m_{13}$ and $m_{11}$, which contain the sine and cosine of the heading respectively, just like we did above. 

The code that extracts the Euler angles from a matrix that only has rotation looks like this:

```c
// Assume the matrix is stored in these variables:
float m11,m12,m13;
float m21,m22,m23;
float m31,m32,m33;

// We will compute the Euler angle values in radians
// and store them here:
float h, p, b;

// Extract pitch from m32, being careful for domain errors with
// asin(). We could have values slightly out of range due to
// floating point arithmetic
float sp = −m32;
if(sp <= −1.0f) { 
	p = −1.570796f; // −pi /2
} else if(sp >= 1.0f) { 
	p = 1.570796 f; // pi /2
} else { 
	p = asin(sp);
}

// Check for the Gimbal lock case, giving a slight tolerance
// for numer ical imprecision
if(fabs(sp) > 0.9999f) {
	
	// We are looking straight up or down.
	// Slam bank to zero and just set heading
	b = 0.0f ;
	h = atan2(−m13, m11);
	
} else {
	
	// Compute heading from m13 and m33
	h = atan2(m31, m33) ;
	// Compute bank from m21 and m22
	b = atan2(m12, m22) ;
	
}
```