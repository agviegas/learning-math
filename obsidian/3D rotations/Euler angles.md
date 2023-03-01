Euler angles consists of representing an orientation as three rotations about three mutually perpendicular axis. Any axis and any order of rotations will work, but the convention is the **heading-pitch-bank** convention.

Let's consider the [[Cartesian space|left-handed y-up 3D cartesian space]]  that we usually use in 3D graphics (and the corresponding direction for 3D rotation). The process to apply Euler angles is the following:

1. Start with the identity orientation.
2. Apply the **heading rotation**: positive local y-axis rotation.
3. Apply the **pitch rotation**: positive local x-axis rotation.
4. Apply the **bank rotation**: positive local z-axis rotation.

![[Pasted image 20230228223748.png|400]]

It's also common to see **yaw-pitch-roll** (from the aerospace field). It's exactly the same thing in the same order: yaw is heading and bank is roll. Other common synonyms are:

- Heading = Yaw = Azimuth
- Pitch = Attitude = Elevation
- Yaw = Roll = Tilt = Twist

It's also common to find this list in inverse order (**roll-pitch-yaw**). This might seem strange, as the order of rotations alters the result. So why list them in inverse order? It turns out that this is the order in which rotations are done inside the computer when converting this to a rotation matrix. But why?

In the definition above we are using the object local coordinates (**body axis**), which change after each rotation. This is called the **intrinsic convention**. But we could also use **fixed axes**, so the rotations would always be "absolute". In this case, to reach the same result, we need to apply the rotations **in the opposite order**. This is called **extrinsic convention** and it's what computers usually do. 

>This is easy to visualize if we forget about yaw. Using the intrisic convention, we would first apply the **heading** (local Y rotation) and then the **pitch** (local X rotation). If we applied the same **pitch** (global X rotation), and then the same **heading** (global Y rotation)  we will reach the same result.

# Aliasing

The representation of a rotation is not unique. This is called **aliasing**, like in the [[Introduction to polar coordinates|polar coordinates]].   In Euler angles we can have aliasing because the 3 angles are not completely independent from each other. 

>Pitching down 135º is the same as heading 180º, pitching down 45º and banking 180º.

Like in polar coordinates, an easy way to solve this is to define a single representation that is the **canonical representation**:

- Limiting the **heading** and the **bank** to (-180º, +180º].
- Limiting the **pitch** to \[-90, +90º].

But even with these limitations, the most famous type of aliasing is not solved. This happens when the **pitch** is +90º and -90º (or, more generally, [when 2 rotation axis align](https://www.youtube.com/watch?v=zc8b2Jo7mno)). Then, the object will keep rotating on the y axis, regardless of the values of **heading** and **bank**. In other words, we have lost a degree of freedom. 

This is case is called **Gimbal lock**. We can solve this aliasing case with one last rule (although this doesn't solve Gimbal interpolation problems, explained below):

- If **pitch** = -90º or **pitch** = 90º, **bank** = 0.

# Interpolation problems

Interpolating angles is a very common operation (e.g. character animation, camera movement, etc). For instance, let's imagine two angles $R_1$ and $R_2$ , and we want to create an animation between them for a time $t$. 

We have to create a function that gives us the rotation for any given time $R(t)$. We could try to apply the linear interpolation (lerp) to the three angles:

$$\Delta R = R_1 - R_0 ~~~~~~~~~~~~~~~~~~~~~~~~ R_t = R_0 + t\Delta R$$

But this has problems because of 3 reasons.

![[Pasted image 20230301001827.png|600]]

1. **Non-canonical angles**

If we have angles that go beyond 180º, the interpolation will result in making multiple revolutions before reaching the final angle. This has an easy solution if we convert all angles to the **canonical angles** described above.

2. **Rotation direction**

Because of the cyclic nature of angles. For instance if we have to interpolate between +170º and -170º, we will get the long rotation instead of the shorter one. We can solve this by limiting the maximum rotation to (-180º, +180º] to find the shortest arc. We can do it like this:

$$f(r) = r − 360º ⌊(r + 180º)/360º⌋$$
Where $⌊~~~~⌋$ is the floor function. And the code looks like this:

```c
float wrapPi(float angle) {
	// Check if already in range. This is not strictly necessary,
	// but it will be a very common situation. We don’t want to
	// incur a speed hit and perhaps floating precision loss if
	// it’s not necessary
	if(fabs(angle) >= PI ) {
		// Out of range. Find out the shortest angle
		const float TWOPPI = 2.0f ∗ PI;
		float revolutions = floor((angle + PI) ∗ (1.0f / TWOPPI));
		angle −= revolutions ∗ TWOPPI;
	}
	return angle ;
}
```

For instance, in the figure above (case 2), instead of rotating 340º, if we apply this function, we would rotate 20º.

3. **Gimbal lock**

This is the worst of the problems because it turns out [it doesn't have a solution](https://www.youtube.com/watch?v=zc8b2Jo7mno). Gimbal lock will make the interpolations [incorrect, following a strange path during the interpolation](https://www.youtube.com/watch?v=zc8b2Jo7mno&t=359s). This happens because if an object is in **gimbal lock**, there are rotations that it can't reach directly without "derrailing away", which looks very weird.

>Unfortunately, this problem is not avoidable, even if we change the order of rotation. As soon as the rotation axes align, there will be **gimbal lock**. This is a problem inherent to using 3 numbers to describe a rotation.

