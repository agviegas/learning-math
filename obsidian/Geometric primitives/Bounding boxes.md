Bounding boxes are one of the most common geometric privimitives used to describe simply the volume of an object. There are 2 types of bounding boxes:

- Axially Aligned Bounding Box (**AABB**). Aligned to the XYZ axes.
- Arbitrarily Oriented Bounding Box (**OBB**).

>Of course, **AABB** are simpler to create and use. But we have to keep in mind that OBB are simply AABB with an orientation. This means that all the operations that we perform on AABB can be applied to OBB applying the orientation. The difference is not in the box itself, but in making the operations in a [[Introduction to matrices#Geometric definition|coordinate space aligned with the bounding box]].

>Here we will focus on 3D **AABB**, but everything can be applied in 2D dropping the 3rd dimension.


# Representing AABB

The two **corners** that define an AABB bounding box are $p_{min}$ and $p_{max}$ .  All the points $[x,y,z]$ inside a bounding box AABB satisfy the inequalities:

$$x_{min} \leq x \leq x_{max} ~~~~~~~~ y_{min} \leq y \leq y_{max} ~~~~~~~~ z_{min} \leq z \leq z_{max}$$

The **center** of the bounding box $c$ is defined by:

$$c=(p_{min}+p_{max})/2$$
The **size vector** $s$ is the vector from $p_{min}$ to $p_{max}$ and contains the width, height and length of the box in each dimension. Sometimes we'll also find the **radius vector**, which is simply $s/2$, or the vector from the center $c$ to $p_{max}$.

$$s=p_{max}-p_{min}$$

>To unambiguously define an AABB we need at least 2 of the 4 vectors $p_{min}$, $p_{max}$, $c$ and $s$. The most common way to define an AABB is through $p_{min}$ and $p_{max}$.


# Computing AABB

Computing a bounding box for a set of given points is quite easy. First, we maximize $p_{min}$ and minimize $p_{max}$. Then, we simply compare them with all the dimensions of all the points, and save the found minimums and maximums.

```c
// Define AABB operations

void AABB3::empty() { 
	min.x = min.y = min.z = FLT_MAX;
	max.x = max.y = max.z = −FLT_MAX ;
}

void AABB3::add (const Vector3 &p) { 
	if (p.x < min.x) min.x = p.x;
	if (p.x > max.x) max.x = p.x;
	if (p.y < min.x) min.y = p.y;
	if (p.y > max.x) max.y = p.y;
	if (p.z < min.x) min.z = p.z;
	if (p.z > max.x) max.z = p.z;
}

// Apply them to compute the AABB of a set of points

const int N;
Vector3 list [N];

AABB3 box;
box.empty();

for (int i = 0; i < N; ++i) { 
	box.add(list[i]);
}
```


# AABB vs Bounding spheres

AABBs have two advantages over bounding spheres:

1. Computing the optimal AABB for a given set of points is easy and fast (linear time). Computing the optimal bounding sphere is much more complex.
2. For many objects, AABB provide a "tighter" (more accurate) volume. There are of course exceptions (e.g. the star in the image below).

![[Pasted image 20230308022359.png|300]]

One problem with AABBs is that they are very sensitive to object orientation. In the image above, the bounding box for the horizontal rifle is very accurate, but when we rotate the rifle, it becomes much worse. If we need more accurate bounding boxes, we could use **OBB** instead (simply applying an orientation to the bounding box).


# Fast OBB to AABB

OBB are more accurate, but AABB are more useful for faster calculations. Having an easy way to convert from one to the other fast would be quite useful.

>A naive approach would be simply computing the AABB for the object. That will work and gives the most accurate result, but if the object has many polygons, it will be slow. 

Instead, we could simply compute the AABB of the OBB itself, not the original object. Of course, we will lose precision and end up with an AABB that is a bit too big (see image below), but this is also much faster because we only deal with 8 vertices. So this method is useful when speed matters more than precission.

![[Pasted image 20230308025243.png|400]]

A possible strategy would be simply applying the [[Inverse|inverse of the transformation]] to the 8 vertices, and then computing the bounding box for them. That would work, but there's a much faster and simpler algorithm that we can use.

>Using just the min and max to compute a new bounding box naively would be wrong, as min could be below max in the conversion from local to global space.

Let's say that the AABB that we want to find is defined by the points $p'_{max}$ and $p'_{min}$ , and the OBB is defined by the points (in local coordinates) $p_{max}$ and $p_{min}$ and has the transformation matrix $M$. If we remember how [[Matrix operations#Matrix - vector product|vector-matrix product works]], we will be applying this operation, where $[x,y,z]$ is any point of the OBB (in local space):

$$\begin{bmatrix} x' & y' & z'  \end{bmatrix} = \begin{bmatrix} x & y & z  \end{bmatrix} \begin{bmatrix} m_{11} & m_{12} & m_{13} \\ m_{21} & m_{22} & m_{23} \\ m_{31} & m_{32} & m_{33} \end{bmatrix} $$
$$x'=m_{11}x+m_{21}y+m_{31}z$$
$$y'=m_{12}x+m_{22}y+m_{32}z$$
$$z'=m_{13}x+m_{23}y+m_{33}z$$


For instance, to find $p'_{min}$ we will want $x'$, $y'$ and $z'$ to have the smallest possible values. How can we make $x'$ have the smallest value? Easy: making the 3 elements of the sum above as small as possible. There are 2 little tricks involved:

1. Because $p_{min}$ and $p_{max}$ are the extreme values in local space, we can simply work with them and ignore the other 6 vertices of the bounding box.
2. Choosing between the min and the max depends on the sign of the component of the matrix. For instance, if we are computing $x'_{min}$ and $m_{11}$ is positive, we will use $x_{min}$. Nevertheless, if $m_{11}$ is negative, we'll use $x_{max}$ (a big negative value is less than a small positive value).

With this simple ideas in mind, here is the code to quickly get the AABB of an OBB:

```c
void AABB3::setToTransformedBox(cons t AABB3 &box , cons t Matrix4x4 &m) {
	
	// Start with the last row of the matrix, which is the translation
	// portion , i.e. the location of the origin after transformation.
	min = max = getTranslation(m);
	
	// Examine each of the 9 matrix elements
	// and compute the new AABB
	
	if(m.m11 > 0.0f) { 
		min.x += m.m11 ∗ box.min.x ; 
		max.x += m.m11 ∗ box.max.x;
	} else { 
		min.x += m.m11 ∗ box.max.x; 
		max.x += m.m11 ∗ box.min.x;
	}
	
	if(m.m12 > 0.0f) { 
		min.y += m.m12 ∗ box.min.x; 
		max.y += m.m12 ∗ box.max.x;
	} else { 
		min.y += m.m12 ∗ box.max.x; 
		max.y += m.m12 ∗ box.min.x;
	}
	
	if (m.m13 > 0.0f) { 
		min.z += m.m13 ∗ box.min.x; 
		max.z += m.m13 ∗ box.max.x;
	} else { 
		min.z += m.m13 ∗ box.max.x; 
		max.z += m.m13 ∗ box.min.x;
	}
	
	if(m.m21 > 0.0f) { 
		min.x += m.m21 ∗ box.min.y; 
		max.x += m.m21 ∗ box.max.y;
	} else {
		min.x += m.m21 ∗ box.max.y; 
		max.x += m.m21 ∗ box.min.y;
	}
	
	if(m.m22 > 0.0f) { 
		min.y += m.m22 ∗ box.min.y; 
		max.y += m.m22 ∗ box.max.y;
	} else { 
		min.y += m.m22 ∗ box.max.y; 
		max.y += m.m22 ∗ box.min.y;
	}
	
	if(m.m23 > 0.0f) { 
		min.z += m.m23 ∗ box.min.y; 
		max.z += m.m23 ∗ box.max.y;
	} else { 
		min.z += m.m23 ∗ box.max.y; 
		max.z += m.m23 ∗ box.min.y;
	}
	
	if(m.m31 > 0.0f) { 
		min.x += m.m31 ∗ box.min.z; 
		max.x += m.m31 ∗ box.max.z;
	} else { 
		min.x += m.m31 ∗ box.max.z; 
		max.x += m.m31 ∗ box.min.z;
	}
	
	if(m.m32 > 0.0f) {
		min.y += m.m32 ∗ box.min.z; 
		max.y += m.m32 ∗ box.max.z;
	} else { 
		min.y += m.m32 ∗ box.max.z; 
		max.y += m.m32 ∗ box.min.z;
	}
	
	if(m.m33 > 0.0f) { 
		min.z += m.m33 ∗ box.min.z; 
		max.z += m.m33 ∗ box.max.z;
	} else { 
		min.z += m.m33 ∗ box.max.z; 
		max.z += m.m33 ∗ box.min.z;
	}
}
```