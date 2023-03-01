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
- They take much more memory (e.g. if we need to store all the rotations in an animation).
- They are difficult for humans to use (humans think in angles).
- Matrices can be ill-formed.

2.  [[Euler angles]]

**Pros**
- Easy for humans to use, because they are just angles, which everyone understands. This makes Euler angles the right choice if we need to show or set the value of rotation nummerically.
- They take little memory (they are the smallest possible representation of an orientation).
- They can be easily compressed (e.g. to a fixed point system). The data loss due to **quantization** is spread evenly and the absolute numeric difference between two values is proportional to the difference perceived (unlike in matrices and quaternions, that need to be able to store very small numbers because the values stored are sines and cosines). 
- Any set of 3 numbers is a valid 3D rotation, which is not the case with matrices and quaternions.

**Cons**
- They are painful to interpolate due to **gimbal lock**, which is unavoidable.

- [[Axis-angle form and exponential maps]]
- [[Quaternions]]



