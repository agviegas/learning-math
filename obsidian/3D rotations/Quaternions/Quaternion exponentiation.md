
We can raise quaternions to a scalar power. This is denoted as $q^t$ and shouldn't be confused with the $\exp$ function (which only takes one argument, not 2).

The quaternion exponentiation means the same as for real numbers. For any scalar, $a^0 = 1$ and $a^1 = a$. As the exponent $t$ varies from 0 to 1, $a^t$ varies from 0 to $a$. The same thing happens with quaternion exponentiation: as $t$ varies from 0 to 1, $q^t$ varies from $[1, 0]$ (unit quaternion) to $q$.

Quaternion exponentition is useful because it allows us to get a "fraction" of a rotation. Remember that "multiplying a quaterion" means applying that rotation. Therefore, multiplying a rotation $n$ times means applying that rotation $n$ times. 

For example, let's imagine a quaternion $q$ that is a positive rotation of 30º around the $x$ axis. Then, $q^3$ applies the $q$ rotation 3 times (positive 90º rotation around the x axis) and $q^{1/3}$ is a positive x-axis 10º rotation. This also works with negative exponents: $q^{-1/3}$ performs a _negative_ x-axis 10º rotation.

>There is one important caveat: quaternions always represent an angular displacement **using the shortest arc**. Multiple spins can't be represented. So $q^8$ is not a positive 240º x-axis rotation, but a 120º negative x-axis rotation. Of course, both rotations end up in the same result, and this is the point: quaternions only capture the end result. **If we care about the total amount of rotation and not only the end result (e.g. angular velocity), quaternions are not the correct tool for the job** and we should use [[Axis-angle form and exponential maps|exponential maps]] instead.

>Many exponential algebraic rules, like $(a^t)^s=a^{ts}$, do not apply to quaternions.

The mathematical definition of quaternion exponentiation is this:

$$q^t = \exp(t \log(q))$$
Although this looks complicated, it's actually very simple. The $log$ operation converts the quaternion to an exponential map format. Then, we multiply the angle by $t$. Then, the $\exp$ function "undoes" what the $\log$ function did, recalculating the new $w$ and $v$.

This is how the implementation in C looks like this. There are 2 things to consider:

>It's important to check for the identity quaternion, as $w=\pm 1$ would cause the `mult` computation to divide by zero. Raising the identity quaternion to any number results in the identity quaternion, so in this case the quaternion would not change.

>When we compute alpha we use the $acos$ function, which always returns a positive angle. This is not a mistake, as any quaternion can be interpreted as having a positive angle of rotation, since negative rotation around an axis is the same as positive rotation around the axis pointing in the opposite direction (remember: $q=-q$).

```c
float w, x, y, z;

// Input exponent
float exponent ;

// Check for the case of an identity quaternion
// This will protect against divide by zero
if(fabs(w) < .9999f) {
	
	// Extract the half angle alpha (alpha = theta/2)
	float alpha = acos(w);
	
	// Compute new alpha value
	float newAlpha = alpha ∗ exponent;
	
	// Compute new w value
	w = cos(newAlpha);
	
	// Compute new xyz values
	float mult = sin(newAlpha) / sin(alpha);
	x ∗= mult;
	y ∗= mult;
	z ∗= mult;
}
```