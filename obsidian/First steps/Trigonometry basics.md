An **angle** is the amount of rotation in a plane. They are usually represented with greek letters like $\theta$ or $\beta$.

<img width="400px" src="https://freesvg.org/img/cont-ring.png" alt="asdf"/>


There are two units to measure angles: 
- **degrees** : 1 revolution = 360º.
- **radians**: 1 revolution = $2\pi$ radians.

#### Trigonometric functions

A circle with radius = 1 is called **unit circle**. The coordinates $(x,y)$ of any point in a unit circle are so useful that they have a name: **cosine** and **sine**, and they are related to the angle $\theta$  that they form with the origin.

<img width="400px" src="https://www.mathsisfun.com/geometry/images/unit-circle-sin-cos-tan.svg" alt="asdf"/>

This can be generalised for any circle of radius $r$ like this.

$$sin(\theta) = \frac y r ~~~~~~~~~ cos(\theta) = \frac x r ~~~~~~~~~ tan(\theta) = \frac y x$$

The inverse of the **sine**, **cosine** and **tangent** are called respectively **cosecant**, **secant** and **cotangent**:

$$csc(\theta) = \frac r y ~~~~~~~~~ sec(\theta) = \frac r x ~~~~~~~~~ tan(\theta) = \frac x y$$

#### Trigonometric identities

The trigonometric funtions have a number of useful relationships called **trigonometric identities**. The most intuitive are the ones based on symmetry:

$$sin(-\theta) = -sin(\theta) ~~~~~~~~~ cos(-\theta) = cos(\theta) ~~~~~~~~~ tan(-\theta) = -tan(\theta)$$

One of the most famous itentities is the pithagorean problem:

$$a^2 + b^2 = c^2$$

<img width="400px" src="https://www.ducksters.com/kidsmath/triangle_pythagorean.gif" alt="asdf"/>

Applying the pithagorean problem to the unit circle, we can deduce the following identities:

$$sin^2(\theta) + cos^2(\theta) = 1 ~~~~~~~~~ 1 + tan^2(\theta) = sec^2(\theta) ~~~~~~~~~ 1 + cot^2(\theta) = csc^2(\theta)$$

If we apply these concepts to the sum and subtraction of two angles, we get these:

$$sin(\theta + \beta) = sin(\theta) \cdot cos(\beta) + cos(\theta) \cdot sin(\beta) $$
$$sin(\theta - \beta) = sin(\theta) \cdot cos(\beta) - cos(\theta) \cdot sin(\beta) $$
$$cos(\theta + \beta) = cos(\theta) \cdot cos(\beta) - sin(\theta) \cdot sin(\beta) $$
$$cos(\theta - \beta) = cos(\theta) \cdot cos(\beta) + sin(\theta) \cdot sin(\beta) $$
$$tan(\theta + \beta) = \frac{tan(\theta) + tan(\beta)}{1 - tan(\theta) \cdot tan(\beta)} $$
$$tan(\theta - \beta) = \frac{tan(\theta) - tan(\beta)}{1 + tan(\theta) \cdot tan(\beta)} $$

Now, if we apply the sum identities to the special case where $\theta$ and $\beta$ are the same, we get this:

$$sin(2 \cdot \theta) = 2 \cdot sin(\theta) \cdot cos(\theta)$$
$$cos(2 \cdot \theta) = cos^2(\theta) - sin^2(\theta) = 2 \cdot cos^2(\theta) - 1 = 1 - 2 \cdot sin^2(\theta) $$
$$tan(2\cdot \theta) = \frac{2 \cdot tan(\theta)}{1 - tan^2(\theta)} $$

Finally, when we need to solve for an arbitrary triangle of sides $(a,b,c)$ and opposite angles $(A,B,C)$ where some sides or angles are unkown. For this, we can use the **law of the sines** or **law of the cosines** depending on the problem:

**Law of the sines**:
$$\frac{sin(A)}{a} = \frac{sin(B)}{b} = \frac{sin(C)}{c} $$

**Law of the cosines**:

$$a^2 = b^2 + c^2 -2bc \cdot cos(A) $$
$$b^2 = a^2 + c^2 -2ac \cdot cos(B) $$
$$c^2 = b^2 + a^2 -2ba \cdot cos(C) $$
