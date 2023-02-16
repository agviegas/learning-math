All transformations presented can be combined or concatenated simply by applying the [[Matrix operations#Matrix - matrix product|matrix product]] So, if we want to apply 2 transformations $A$ and $B$, we can simply $AB$. Generally, any complex tranformation can be expressed as a concatenation of simple ones.

**The other of transformation matters**. Matrix product is not conmutative, and this means that the transformations will apply in the order that they are set. This makes sense, because if we rotate and scale we'll get a different output than if we scale and rotate. 

>The most important thing to keep in mind whether we are using [[Matrix operations#Matrix - vector product|row or column vectors]], as the order is the opposite. For **row vectors**, sequence of transformation matrices are applied from left to right ($\vec v ABC$) while in **column vectors** the transformation sequence needs to be from right to left ($CBA\vec v$). 

___
[Here](https://webgl2fundamentals.org/webgl/lessons/webgl-2d-matrices.html) is an interesting example for WebGL at the end of the article (we should keep in mind that WebGL is a bit [special](https://webgl2fundamentals.org/webgl/lessons/webgl-matrix-vs-math.html)).
___

Thanks to the **associative** property of the matrix product, we can precompute transformation matrices that contain multiple transformations, and then just keep adding more and more transformations with further multiplications.