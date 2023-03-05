Intuitively we know that the "orientation" of an object tells us what direction the object is facing. But "orientation" is not the same as "direction". For instance, a vector has a direction but not an orientation (we can rotate the vector around its axis and nothing changes, because it has no thickness). 

>A **direction** can be parametrized in 3D with just [[3D polar space|2 numbers]], while an orientation needs at least 3 numbers (asumming we are using **Euler angles**).

Just like translation, orientation must be always given from a reference point (often called the **identity rotation** or **home rotation**). The amount of rotation is known as **angular displacement**.

There are many ways of describing an orientation in 3D space, and each one has its pros and cons. 

>The common strategy is to store rotation in eulers and/or quaternions, and then have a matrix that is re-computed every time the other data updates, and that is then combined with the rest of the transformations (translation, scale, etc).

1. [[Linear transformations#Rotation|Matrix orientation]]

**Pros**:
- **Rotation of vectors is directly available**.
- Format used by graphic APIs.
- **Easily concatenation of multiple rotations and inversion**.
- **Easy concatenation with other transformations**.
- Unique representation for a given rotation (no aliasing).

**Cons**:
- **They can't interpolate** (so we must use other system for interpolations/animations).
- They **take more memory** (e.g. if we need to store all the rotations in an animation).
- They are **difficult for humans to use** (humans think in angles).
- Matrices can be ill-formed (creep matrices).
- Not easy to understand, although easier than exponential maps and quaternions.

2.  [[Euler angles]]

**Pros**
- **Easy for humans to understand**, because they are just angles, which everyone understands. This makes Euler angles the right choice if we need to show or set the value of rotation nummerically.
- They **take little memory** (they are the smallest possible representation of an orientation).
- They can be **easily compressed** (e.g. to a fixed point system). The data loss due to **quantization** is spread evenly and the absolute numeric difference between two values is proportional to the difference perceived (unlike in matrices and quaternions, that need to be able to store very small numbers because the values stored are sines and cosines). 
- **Any set of 3 numbers is a valid 3D rotation**, which is not the case with matrices and quaternions.

**Cons**
- They are painful to interpolate due to **gimbal lock**, which is unavoidable.
- **Can't rotate points between coordinate spaces directly**, must always convert to a rotation matrix.
- **Can't invert a rotation** easily.
- **Can't concatenate multiple rotations**. 
- **Aliasing**.

- [[Axis-angle form and exponential maps]]

**Pros**
- Very useful for angular velocity when we need to support **multiple spins**.
- **Easy and fast inversion of rotations**.
- **Possible interpolation**, with some singularitites, but much better than Euler.
- **Can't become invalid**.
- Only three numbers and easy compression / quantization (like Euler angles).

**Cons**
- **Can't rotate points between coordinate spaces directly**, must always convert to a rotation matrix.
- **Can't concatenate multiple rotations**. 
- **Aliasing** (but easier to solve than Euler angles).
- Difficult to understand.

- [[Quaternions]]

**Pros**
- The only method that guarantees **reliable quality interpolations** (useful for animations).
- **Fast concatenation of rotations and inversion** (although the difference nowadays with matrix operations is not so clear).
- Fast conversion from and to matrix form.
- **Only four numbers** (smaller than matrices, bigger than Euler angles).
- Only two distinct representations for a given rotation (no aliasing).

**Cons**
- **Can rotate points between coordinate spaces directly**, but usually this is not used. Instead, they are converted to a rotation matrix.
- **Can become invalid** because of bad input data or accumulated error. We can solve this by regularly normalizing the quaternions to make sure that they remain unit (magnitude=1).
- The **most difficult system** for humans to work with.
- Can't compress / quantize well directly.

