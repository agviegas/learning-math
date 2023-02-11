
**Functions** are a special kind of [[Equations|equation]] of two real variables (`x,y`), so that for each value of `x` there is a single value of `y`. For example:

$$ y = x + 3 $$

The same can be expressed with **functional notation**, which expresses that the input value is $x$ and the output value is $y$:

$$ f(x) = x + 3 $$

```
Functions of degree 1 are also called linear functions and represent straight lines.
```

All linear functions or straight lines that satisfy a given set of conditions are called **family of lines**. They can be defined by leaving one of the elements of a linear function as a variable. For example, given a variable a: 

$$ f(x) = 2x + a $$

This defines a family that includes all straight lines with slope 2.


# Rank and domain

The **domain** of a function is all the real values that we can give to `x` without `y` being undefined. The **range** of a function is all the values that `y` can reach. 

Range and domain can be expressed with bracket notation (if the limit number is not included) or parentheses (if it is not). For example, [4, 7] is all numbers from 4 to 7 (but not including 7).

```
When a function is represented as a line on a two-dimensional Cartesian axis graph, the domain is all x-values and the graph is all y-values.
```

The three most common cases of range limitation are:

- `x` cannot have any value that results in a null denominator. In this case, both the range and the domain are all numbers from minus infinity to plus infinity minus 0.

$$ f(x) = \frac 1 x $$
- `x` cannot have any value that results in a negative root.
$$ f(x) = \sqrt{x} $$
- `x` cannot have any value that results in a zero logarithm, or a logarithm equal to or less than zero if the base is positive. In this example x must necessarily be greater than zero; that is, the domain of the function is all those values that make x greater than zero. 
$$ f(x) = \log x $$
$$ x > 0 $$
When the domain is limited, generally the range is also limited. There are cases where the domain is infinite but the range is bounded. In the following example, the domain can be any value but the range can only be values greater than zero.
$$ f(x) = 10^x $$
Note that another way of expressing a function is as a sequence of points in space. In the following example the domain is 0 and 3 and the range is 1 and 4.
$$ f(x) = (0, 1), (3, 4) $$

# Symmetry

Functions can be classified according to their symmetry into three types:

- **Even**: symmetric with respect to `y`. This means that:

$$ f(x) = f(-x) $$

- **Odd**: symmetrical about the origin. This implies:

$$ -f(x) = f(-x) $$

- **Non-symmetric**: does not meet either of the two conditions.


# Slope

The **slope** of a function is its slope at each point, i.e. how much `y` changes for each unit of `x`. It is denoted by the letter `m`.

Given the function of a straight line, its slope can be determined by taking any two points `(x, y)` and applying the following function:
$$ m = \frac {y_2 - y_1} {x_2 - x_1} = \frac {\triangle y }{\triangle x} $$

```
Vertical lines (parallel to the y-axis) are not functions and have no definite slope. On the other hand, horizontal lines (parallel to the x-axis) have zero slope.
```

Using this formula, and leaving one of the two points as variables `(x, y)`, the function of a straight line can be expressed as a function of a point and a slope:
$$ y - y_1 = m (x - x_1) $$
For example, a line with slope 3 and passing through the point (-6, 1) can be expressed as follows:
$$ y - 1 = 3 (x + 6) $$
$$ f(x) = 3x + 19 $$
The function can be simplified if the point chosen is the point of intersection with the y-axis. In this case, `y1` is usually called `b` by convention.
$$ y - y_1 = m (x - x_1) $$
$$ y - y_1 = m (x - 0) $$
$$ y = m x + y_1 $$
$$ y = m x + b $$

```
Given a straight line function with slope m, a parallel line will also have slope m, and a perpendicular line will have slope -1/m.
```


# Distance

A finite piece of any line is called a **segment**. A segment is always defined by two points. Its length can be easily found with the [[Trigonometry|Pythagorean theorem]].


# Composite functions

Functions can be composed from other simple functions using domain notation. The idea is simple: we define in which domain which function applies.

For example, we can have a function that is determined by one formula when its domain is greater than or equal to zero and by another when it is greater.


# Inverse

The function that "undoes" the transformation or rule of the original function is called the **inverse** of a function. It is the function resulting from "exchanging" `x` and `y` and clearing `y`. 

Functions are only invertible if for every value of `x` there is a value of `y` and vice versa. This excludes all quadratic functions. Otherwise, functions can only be invertible if their domain is restricted.