The name Euler is attached to a lot of stuff related to rotations (like the [[Euler angles]]). His name is also attached to **Euler's rotation theorem**, which says that any 3D angular displacement can be done with a single rotation if we chose the axis carefully. 

>In other words, given two orientations $R_1$ and $R_2$, there is an axis $\hat n$ that allows us to go from one to the other with a single rotation.

Euler's rotation theorem leads to two related methods to describe a rotation. The first one is called **axis-angle form** and is simply describing a rotation by an angle $\theta$ and the direction of the rotation axis throught the unit vector $\hat n$.

Because $\hat n$ has unit length, we can multiply it by $\theta$ without losing information, resulting in the single vector $e = \theta \hat n$. This has the intimidating name **exponential map**. The angle can be deduced from the length of $e$. This is more elegant that the **axis-angle form** (three numbers instead of four), avoids some singularities and is easier to interpolate and differentiate.

This method of describing a rotation is less common than other formats. The biggest strenght of this system is interpolation, because we can find the "fraction" or "multiple" of a rotation as easily as multiplying $\theta$ or $e$ by a factor. This is very handy for interpolations and animations.

>In fact, this is what [[Quaternions]] use under the hood for interpolation. Quaternions can also do this using **slerp**, but it's more convoluted and without the ability of intermediate results to store rotations beyond 180º.

**Exponential maps** are more common than **angle-axis form**, and they usually used to store **angular velocity**, mainly because they are very easy to differentiate and can represent multiple rotations easily.

Like [[Euler angles]], this form of rotation also have aliasing, but they are way easier to deal with:

- For $\theta = 0$ (no rotation), the axis is irrelevant. In the **exponential map**, the multiplication of $\theta$ elegantly makes the information of the axis $\hat n$ vanish.
- If both $\theta$ and $\hat n$ are negative. Again, the **exponential map** gets rids of this in the multiplication of $\theta$ and $\hat n$.

Other types of aliasing (like having an angle greater than 360º) could be dispatched similarly as we did for [[Euler angles]], but this is not always desirable. If we are using **exponential maps** to describe an **angular velocity**, it's not the same saying that an object is rotating 720º/second than 1080/second. In this case, we won't want to create a **canonical form**, as we would be losing information.
