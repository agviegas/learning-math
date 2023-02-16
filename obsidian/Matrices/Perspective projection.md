When we interpret a [[Homogeneus space|4D vector in 3D]], we divide by $w$. If we play with the value of $w$ wisely, we can use that operation to encapsulate the **perspective projection** operation.

Perspective projection is similar to the [[Linear transformations#Orthographic projection|orthographic projection]] (both project to a 2D plane called **projection plane**), but all the projection lines converge to a point called **center of projection**. This projection system is sometimes called [pinhole camera](https://en.wikipedia.org/wiki/Pinhole_camera_model).

![[Pasted image 20230216192502.png]]

The problem with this system is that the image inversion generates some unnecessary complexity. So what we do in 3D apps is to move the **projection plane** in front of the **projection center**, which would be impossible for a camera, but is possible in the 3D universe that we create. 

Assuming that the **projection plane** is $(x,z)$, and the distance between the **projection plane** and the **projection center** is called $d$, we can generalize the [[Homogeneus space|homogeneus projection]] and define the projected position of any 3D point into the plane for any $d$. 

>The idea is simple: $z$ will have the value $d$, so we need to divide by $z$ and multiply by $d$. This operation consists of "scaling" the vector that goes from the origin to $p$, so we need to make the same operation for $x$ and $y$ :

$$p'=\begin{bmatrix} x' & y' & z' \end{bmatrix} = \begin{bmatrix} dx/z & dy/z & d \end{bmatrix} $$

![[Pasted image 20230216192757.png]]

Now, wouldn't it be great to encapsulate this in a matrix, so that we can concatenate this with the rest of 3D transformations? To find that matrix, we need to be able to express that point as an **homogeneus vector** (with the 4th dimension $w$). We need to manipulate the previous equation a little bit:

$$ \begin{bmatrix} dx/z & dy/z & d \end{bmatrix} = \begin{bmatrix} dx/z & dy/z & dz/z \end{bmatrix} = \frac {\begin{bmatrix} x & y & z \end{bmatrix}} {z/d} $$

Now we have a common denominator for all components of the vector, so we can easily find the [[Homogeneus space|4D homogeneous vector that is projected to this 3D point]]:

$$\begin{bmatrix} x & y & z & z/d \end{bmatrix}$$

So the matrix that we are looking for multiplies a homogeneus vector $\begin{bmatrix} x & y & z & 1 \end{bmatrix}$ and returns the homogeneus vector $\begin{bmatrix} x & y & z & z/d \end{bmatrix}$. The matrix that does that is this:

$$\begin{bmatrix} x & y & z & 1 \end{bmatrix} \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 1/d \\ 0 & 0 & 0 & 1  \end{bmatrix} = \begin{bmatrix} x & y & z & z/d \end{bmatrix}$$

Here we have our 4x4 projection matrix. It's important to note that **this matrix doesn't actually perform the perspective transform**, it just computes the proper denominator into $w$. The actual perspective projection happens when we divide all the components by $w$.

>This look overly complicated. Wouldn't it be easier to just divide $(x,y,z)$ by $z$ and multiply by $d$? Yes, but encapsulating this transformation in this matrix makes concatenation with other transformations possible. Besides, this is not that complex: we just did exactly the same [[Homogeneus space|homogeneus space projection]], but backwards.

The perspective projection matrix in real graphics APIs does more than just copying $z$ into $w$. For instance, it usually normalizes the **camera frustum** so that it fits the **clip space** (which go from -1 to +1).