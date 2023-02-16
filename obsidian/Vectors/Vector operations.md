
# Vector - scalar product

$$a \vec v = \vec v a  = a \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} a ~ v_1 \\ a ~ v_2 \\ a ~ v_3 \end{bmatrix} $$

The vector scalar product results in a new vector where each component has been multiplied by the scalar. It's **conmutative**. Geometrically speaking, this operations modifies the vector's **magnitude**.
<img width="300px" src="https://d138zd1ktt9iqe.cloudfront.net/media/seo_landing_files/9591b58e-b010-48b3-a0b3-e0bc91187a62" alt="asdf"/>

___
The **additive inverse** of a vector $\vec v$ is $-\vec v$ . The vector $-\vec v$ has the same magnitude and opposite direction as $\vec v$. In other words, if $0$ is the zero vector:
$$\vec v + -(\vec v) = 0$$
___

Vectors can't be the denominator, as that operation doesn't make sense. But dividing a vector by a scalar is exactly the same as multiplication if we consider the following:

$$\frac {\vec v}{a} = \frac {1}{a} \vec v $$
# Vector - vector sum

The sum of two vectors results in a new vector where each component is the sum of the previous respective components. Both vectors should have the same **dimension**.

$$\vec a + \vec b = \begin{bmatrix} a_1 \\ a_2 \\ a_3 \end{bmatrix} + \begin{bmatrix} b_1 \\ b_2 \\ b_3 \end{bmatrix} = \begin{bmatrix} a_1 + b_1 \\ a_2 + b_2 \\ a_3 + b_3 \end{bmatrix} $$
The geometric meaning of this is applying the second vector displacement to the first vector, thus resulting in a total displacement. 

<img width="300px" src="https://tikz.net/files/vector_sum-001.png" alt="asdf"/>

The subtraction of two vectors is identical if we consider the following formula. The sum is **conmutative**, but the subtraction is not. In fact, $\vec a - \vec b$ will result in a vector that has the same **magnitude** and opposite **direction** as the result of $\vec b - \vec a$.
$$\vec a - \vec b = \vec a + (-1) \cdot \vec b $$

# 2 points to vector

A vector can be defined from two points with the following formula:

$$\vec {PQ} = Q - P = \begin{bmatrix} q_1 - p_1 \\ q_2 - p_2 \\ q_3 - p_3 \end{bmatrix} $$


<img width="300px" src="https://math.lakschool.com/en/themen/vektor/images/vektor_verschiebung.png" alt="asdf"/>

>The opposite operation $P - Q$ would result in a vector with the opposite direction and same module.

# Magnitude of a vector

The magnitude (length) of a vector of $n$ dimensions can be easily computed using the [[Trigonometry#Trigonometric identities|pithagorean theorem]]:

$$||v|| = \sqrt{\sum^n_{i=1}v_i^2}$$
So, for instance, for a 3 dimensional vector:

$$||v|| = \sqrt{v_1^2 + v_2^2 + v_3^2}$$

<img width="300px" src="https://math.lakschool.com/en/themen/vektor/images/vektor_betrag.png" alt="asdf"/>

>This can be used to compute the distance between two points in space. We can just create a vector between the two points and compute its **magnitude**.


# Vector normalization

Normalizing a vectors means computing a **unit vector** with the same direction. A **unit vector** is a vector whose magnitude is 1. They are very useful because they don't contain **magnitude** information: just **direction**. 

>They are sometimes known as **normalized vectors**, **normal vectors** or **normals**, but we have to be careful with this therminology. First, because "normal" also means "perpendicular"; secondly because it's used to refer specifically to the normal buffer of a geometry, as it's made vectors that are both unit and perpendicular to the faces.

We can normalize a vector by dividing it by its **magnitude**:

$$\hat{v} = \frac{\vec v}{||v||}  $$
>The zero vector can't be normalized because it would result in a division by zero.


# Vector dot product

The **dot product** (or **inner product**) of two vectors is the sum of the product of their respective components. Both vectors must have the same dimensions, the operation is **conmutative**, **distributive** and it results in a scalar.

$$\vec a \cdot \vec b = \vec b \cdot \vec a = \sum^n_{i=1}a_ib_i$$
For instance, for 2 3-dimensional vectors:

$$\vec a \cdot \vec b = a_1b_1 + a_2b_2 + a_3b_3$$


This operation has a very interesting property: it can be expressed in relationship with the angle $\theta$ formed by the vectors:

$$\vec a \cdot \vec b = ||a||~||b||~cos(\theta)$$

Why? It's actually quite easy. Let's see the easiest possible example, where b is in the $x$ axis (which means that $b_x = ||b||$):

$$\vec a = \begin{bmatrix} a_x \\ a_y \end{bmatrix} ~~~~~~~~~ \vec b = \begin{bmatrix} b_x \\ 0 \end{bmatrix}$$
$$\vec a \cdot \vec b = a_x \cdot b_x + b_y \cdot 0 = a_x \cdot b_x = ||a||cos(\theta) \cdot b_x = ||a||~||b||~cos(\theta) $$



<img width="500px" src="https://d138zd1ktt9iqe.cloudfront.net/media/seo_landing_files/geometrical-meaning-of-dot-product-1626103065.png" alt="asdf"/>

In other words, the **dot product** is proportional to the lengths of the two vectors and the cosine. This is very convenient, because if the two vectors are unit vectors, then:

$$\hat{a} \cdot \hat{b} = cos(\theta)  $$

>Which means that the **dot product** will give us information of _how alike_ the directions of these vectors are. The more the look at the same direction, the higher the result:
>
>- If the vectors are parallel: $cos(0) = 1$
>- If the vectors are perpendicular: $cos(90) = 0$
>- If the vectors are opposite: $cos(180) = -1$


This is also very useful for computing: 

1. The angle between two vectors (clearing the general formula and the unit vector formula respectively):
$$\theta = acos(\frac{\vec a \cdot \vec b}{||a||~~||b||}) = acos(\hat{a} \cdot \hat{b})$$
2. The projection from a vector $\vec a$  into another vector $\vec b$ (clearing the 2D example above):

$$\vec {ab} = ||a||cos(\theta) = \frac{\vec a \cdot \vec b}{||b||}$$

# Vector cross product

The **cross product** could be seen, in some way, as the opposite to the **dot product**. The **dot product** results in a scalar, is **conmutative** and gives information of _how alike_ the directions of these vectors are. On the other hand, the **cross product** results in a vector, is **anticonmutative** and gives information of _how different_ the directions of these vectors are.

> The **cross product** can be applied only between 3D vectors and creates a new vector that is perpendicular to the other two.

<img width="300px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Cross_product.gif/220px-Cross_product.gif" alt="asdf"/>

The formula is the following:

$$\vec a \times \vec b = \begin{bmatrix} a_x \\ a_y \\ a_z \end{bmatrix} \times \begin{bmatrix} b_x \\ b_y \\ b_z \end{bmatrix} = \begin{bmatrix} a_yb_z \\ a_zb_x \\ a_xb_y \end{bmatrix}$$

This operation is **anticonmutativity** and **not associative**: 
$$\vec a \times \vec b = -(\vec b \times \vec a)$$
$$\vec a \times (\vec b \times \vec c) \neq (\vec a \times \vec b) \times \vec c$$

The **magnitude** of the resulting vector is proportional to the length of the two vectors and is affected by the angle that they form:

$$||\vec a \times \vec b|| = ||a||~||b||~sin(\theta)$$

This means that if both vectors are **unit vectors**, the **magnitude** of the resulting vector will range between 1 (if both vectors are perpendicular) and 0 (if they are parallel).

$$||\hat a \times \hat b|| = sin(\theta)$$
>In 3D apps, the direction of the resulting vector will vary depending on the [[Cartesian space|hand system]] that we are using in that space.