All transformations presented can be combined or concatenated simply by applying the [[Matrix operations#Matrix - matrix product|matrix product]] So, if we want to apply 2 transformations $A$ and $B$, we can simply $AB$. Generally, any complex tranformation can be expressed as a concatenation of simple ones.

**The other of transformation matters**. Matrix product is not conmutative, and this means that the transformations will apply in the order that they are set. This makes sense, because if we rotate and scale we'll get a different output than if we scale and rotate. There are 2 ways to look at this. [Here](https://webgl2fundamentals.org/webgl/lessons/webgl-2d-matrices.html) both perspectives are illustrated at the end of the article.

- **From right to left** (if we think of the transformation as moving an object around
- **From left to right** (if we think of the transformation as transforming coordinate systems). 

Thanks to the **associative** property of the matrix product, we can precompute transformation matrices that contain multiple transformations, and then just keep adding more and more transformations with further multiplications.