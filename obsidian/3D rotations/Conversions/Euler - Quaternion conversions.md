# Euler to quaternion

To convert Euler angles to quaternions we can use a similar technique as for [[Euler - Matrix conversions#Euler to matrix|generating a rotation matrix from Euler angles]]: first we convert the three rotations to simple quaternions and then we concatenate them. Therefore, we can define **heading**, **pitch** and **bank** like quaterions:

$$h = \begin{bmatrix} \cos(h/2) \\ \begin{pmatrix} 0 \\ \sin(h/2) \\ 0  \end{pmatrix}  \end{bmatrix}, ~~~~~~~~ p = \begin{bmatrix} \cos(p/2) \\ \begin{pmatrix} \sin(p/2) \\ 0 \\ 0  \end{pmatrix}  \end{bmatrix}, ~~~~~~~~ b = \begin{bmatrix} \cos(b/2) \\ \begin{pmatrix} 0 \\ 0 \\ \sin(b/2)  \end{pmatrix}  \end{bmatrix}$$

Now we just need to concatenate them in the correct order. We are going to use [[Euler angles|fixed axes]], so the order needs to be bank -> pitch -> heading. Nevertheless, [[Quaternions basic operations|quaternion multiplication]] is from right to left, so we actually need to multiply these quaternions like this:

$$hpb = \begin{bmatrix} \cos(h/2) \cos (p/2) \cos(b/2) + \sin(h/2) \sin(p/2) \sin(b/2) \\ \begin{pmatrix} \cos(h/2) \sin(p/2) \cos(b/2) + \sin(h/2) \cos(p/2) \sin(b/2) \\ \sin(h/2) \cos(p/2) \cos(b/2) - \cos(h/2) \sin(p/2) \sin(b/2) \\ \cos(h/2) \cos(p/2) \sin(b/2) - \sin(h/2) \sin(p/2) \cos(b/2)  \end{pmatrix}  \end{bmatrix}$$

# Quaternion to Euler

Knowing how to convert [[Quaternion - Matrix conversions#Quaternion to matrix|a quaternion to a matrix]] and [[Euler - Matrix conversions#Matrix to Euler|a matrix to Euler angles]], we can just use these both steps to make Euler angles from quaternions. If we make the whole process, we end up with the following formular to get  **pitch**, **heading** and **bank**:

$$p = \arcsin(-2(yz-wx))$$
Now, similarly to when we extract Euler angles from matrices, we need to assume two cases: when $\cos p \neq 0$ and when $\cos p = 0$ (**Gimbal lock**).

For $\cos p \neq 0$: 

$$h = atan2(xz+wy, \frac 12 - x^2 - y^2)$$
$$b = atan2(xy+wz, \frac 12 - x^2 - z^2)$$

For $\cos p = 0$ (**Gimbal lock**). Like in the  [[Euler - Matrix conversions#Matrix to Euler|matrix-Euler example]], we arbitrarily decide that all the rotation will be on the heading, and therefore the bank is going to be zero.

$$h = atan2(-xz+wy, \frac 12 - y^2 - z^2)$$
$$b = 0$$

And this is how the code looks like:

```c
// Input quaternion
float w, x, y, z;

// Output Euler angles (radians)
float h, p, b;

// Extract sin (pitch)
float sp = −2.0f ∗ (y∗z − w∗x);

// Check for Gimbal lock , givings light tolerance
// for numerical imprecision
if(fabs(sp) > 0.9999f) {
	// Looking s t r a i g h t up or down
	p = 1.570796 f ∗ sp ; // pi /2
	// Compute heading , slam bank to zero
	h = atan2(−x∗z + w∗y , 0.5 f − y∗y − z∗z ) ;
	b = 0.0 f ;
} else {
	// Compute angles
	p = a s in ( sp ) ;
	h = atan2 ( x∗z + w∗y , 0.5 f − x∗x − y∗y ) ;
	b = atan2 ( x∗y + w∗z , 0.5 f − x∗x − z∗z ) ;
}
```