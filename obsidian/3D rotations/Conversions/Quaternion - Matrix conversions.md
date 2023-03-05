
# Quaternion to matrix

There are many ways to convert a quaternion to a rotation matrix. The most common way is to expand the multiplication $qvq^{-1}$ , Instead, in this case we'll use the geometric interpretation of the components of the quaternion. Since a quaternion is just an encoded version of an [[Axis-angle form and exponential maps|axis-angle rotation]], which is just a rotation around an arbitrary axis, we can create a matrix that makes a rotation around an arbitrary axis and is constructed from an arbitrary quaterion $[w, (x, y, z)]$. 

This matrix looks like this. It's not important to understand this to be able to use it effectively, and the deduction is somewhat convoluted.

$$\begin{bmatrix}1 - 2y^2 - 2z^2 & 2xy + 2wz & 2xz - 2wy \\ 2xy - 2 wz & 1 - 2x^2-2z^2 & 2yz + 2wx \\ 2xz + 2wy & 2yz - 2wx & 1 - 2x^2 - 2y^2 \end{bmatrix}$$

# Matrix to quaternion

To extract a quaternion out of a matrix, we can simply reverse-engineer the previous step. We get these equations:

$$w = \frac{\sqrt{m_{11}+m_{22}+m_{33} + 1}}{2}$$
$$x = \frac{\sqrt{m_{11}-m_{22}-m_{33} + 1}}{2}$$
$$y = \frac{\sqrt{-m_{11}+m_{22}-m_{33} + 1}}{2}$$
$$z = \frac{\sqrt{-m_{11}-m_{22}+m_{33} + 1}}{2}$$

But this has a problem: how do we know if we should take the positive or negative root? Because for quaternions $q=-q$ , we can choose one of the four equations and just take the positive value, and then solve for the rest using these equations:

$$m_{12} + m_{21} = 4xy$$
$$m_{12} - m_{21} = 4wz$$
$$m_{31} + m_{13} = 4xz$$
$$m_{31} - m_{13} = 4wy$$
$$m_{23} + m_{32} = 4yz$$
$$m_{23} - m_{32} = 4wx$$

But which one should we use? In other words, for which component should we solve for first? We could choose an arbitrary one (e.g. use the equation for $w$ and then use the other 6 equations to solve for the rest), but this doesn't work. If $w$ is 0, we won't be able to solve, and if $w$ is very small, we will have nummerical stability issues. 

A smarter strategy is to determine which element ($x$, $y$, $z$ or $w$) has the absolute biggest value (for which we don't need to compute the square root) and always choose that one. So depending on the equation we choose, we solve like this:

$$w = \frac{\sqrt{m_{11}+m_{22}+m_{33} + 1}}{2} \rightarrow x = \frac {m_{23}-m_{32}}{4w}, y=\frac {m_{31}-m_{13}}{4w}, z=\frac {m_{12}-m_{21}}{4w}$$
$$x = \frac{\sqrt{m_{11}-m_{22}-m_{33} + 1}}{2} \rightarrow w = \frac {m_{23}-m_{32}}{4x}, y=\frac {m_{12}+m_{21}}{4x}, z=\frac {m_{31}+m_{13}}{4x}$$
$$y = \frac{\sqrt{-m_{11}+m_{22}-m_{33} + 1}}{2} \rightarrow w = \frac {m_{31}-m_{13}}{4y}, x=\frac {m_{12}+m_{21}}{4y}, z=\frac {m_{23}+m_{32}}{4y}$$
$$z = \frac{\sqrt{-m_{11}-m_{22}+m_{33} + 1}}{2} \rightarrow w = \frac {m_{12}-m_{21}}{4z}, x=\frac {m_{31}+m_{13}}{4z}, y=\frac {m_{23}+m_{32}}{4z}$$

And the code looks like this:

```c
// Input matrix:
float m11,m12,m13;
float m21,m22,m23;
float m31,m32,m33;

// Output quaternion
float w, x, y, z;

// Determine which of w, x, y, or z has the largest absolute value
float fourWSquaredMinus1 = m11 + m22 + m33;
float fourXSquaredMinus1 = m11 − m22 − m33;
float fourYSquaredMinus1 = m22 − m11 − m33;
float fourZSquaredMinus1 = m33 − m11 − m22;

int biggestIndex = 0;
float fourBiggestSquaredMinus1 = fourWSquaredMinus1;

if(fourXSquaredMinus1 > fourBiggestSquaredMinus1) { 
	fourBigges tSquaredMinus1 = fourXSquaredMinus1;
	biggestIndex = 1;
}

if(fourYSquaredMinus1 > fourBiggestSquaredMinus1) { 
	fourBigges tSquaredMinus1 = fourYSquaredMinus1 ;
	biggestIndex = 2;
}

if(fourZSquaredMinus1 > fourBiggestSquaredMinus1) { 
	fourBiggestSquaredMinus1 = fourZSquaredMinus1 ;
	biggestIndex = 3;
}


// Perform square root and division
float biggestVal = sqrt(fourBiggestSquaredMinus1 + 1.0f) ∗ 0.5f;
float mult = 0.25f / biggestVal;

// Apply table to compute quaternion values
switch(biggestIndex) {
	
	case 0:
		w = biggestVal;
		x = (m23 − m32) ∗ mult;
		y = (m31 − m13) ∗ mult;
		z = (m12 − m21) ∗ mult;
	break;
	
	case 1:
		x = biggestVal;
		w = (m23 − m32) ∗ mult;
		y = (m12 + m21) ∗ mult;
		z = (m31 + m13) ∗ mult;
	break ;
	
	case 2:
		y = biggestVal;
		w = (m31 − m13) ∗ mult;
		x = (m12 + m21) ∗ mult;
		z = (m23 + m32) ∗ mult;
	break ;
	
	case 3:
		z = biggestVal;
		w = (m12 − m21) ∗ mult;
		x = (m31 + m13) ∗ mult;
		y = (m23 + m32) ∗ mult;
	break ;
}
```