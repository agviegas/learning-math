Intuitively we know that the "orientation" of an object tells us what direction the object is facing. But "orientation" is not the same as "direction". For instance, a vector has a direction but not an orientation (we can rotate the vector around its axis and nothing changes, because it has no thickness). 

>A **direction** can be parametrized in 3D with just [[3D polar space|2 numbers]], while an orientation needs at least 3 numbers (asumming we are using **Euler angles**).

Just like translation, orientation must be always given from a reference point (often called the **identity rotation** or **home rotation**). The amount of rotation is known as **angular displacement**.

There are many ways of describing an orientation in 3D space, and each one has its pros and cons:

1. [[Linear transformations#Rotation|Matrix orientation]]

**Pros**:
- Rotation of vectors is directly available.
- Format used by graphic APIs.
- Allows easy concatenation of multiple rotations.
- Allows easy rollback (using the inverse matrix).

**Cons**:
- They take much more memory (e.g. if we need to store all the rotations in an animation)
- They are difficult for humans to use (humans think in angles)
- Matrices can be ill-formed

2.  [[Euler angles]]



- [[Axis-angle and exponential map]]
- [[Quaternions]]



