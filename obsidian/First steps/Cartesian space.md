
3D math is all about measuring locations, distances and angles in a 3D space, and this is usually done in a **cartesian coordinate system**. 

A **2D cartesian coordinate system** is a space defined by 2 orthogonal axis $(x,y)$ where:

- The intersection of axis is called **origin**.
- Any point of that space can be expressed as two numbers called **coordinates**. A **coordinate** is the distance of the axis projection of that point to the **origin**.
- The arrangment of axis doesn't matter (e.g. we could make $x$ look down and $y$ look left). Any arrangement is reachable from the rest of arrangements through rotation in the $x$, $y$ or $z$ axis, which means that we are always in the same coordinate system.

<img width="300px" src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Cartesian-coordinate-system.svg/1024px-Cartesian-coordinate-system.svg.png" alt="asdf"/>

A **3D cartesian coordinate system** $(x,y,z)$ usually looks like this:

<img width="300px" src="https://buzzcoder.gitbooks.io/codecraft-python/content/assets/3D_coordinate_system.png" alt="asdf"/>
It has some difference to the 2D cartesian coordinate system:

- In 3D, the coordinates are the distance of a point to the zero-plane for that dimension. For instance, the $x$ coordinate is the distance of that point to the $yz$ plane.
- The arrangment of the axis matter, because not all arrangements are reachable from the rest of arrangements through rotation. There are 2 types of systems: **left hand** and **right hand**. We can use our hands to idenfity the type of a system:

<img width="350px" src="https://www.oreilly.com/api/v2/epubs/9781788830409/files/assets/a465e4c5-b6ca-4006-a40e-1aa9ad2ebc5d.png" alt="asdf"/>

>One of the most important differences between **left hand systems** and **right hand systems** is the definition of a "positive rotation" (clockwise vs counter-clockwise). We can easily figure the positive rotation direction using our right or left hand respectively:

<img width="300px" src="https://www.researchgate.net/profile/Pascal-Man/publication/257891177/figure/fig18/AS:268437813461026@1441011970994/Right-handed-rotation-with-the-thumb-of-the-right-hand-pointing-along-the-rotation-axis.png" alt="asdf"/>

We can convert a system to the other by multiplying an axis by -1 or by swapping 2 coordinates. 