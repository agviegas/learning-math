
An equality between two entities with one or more variables is called an **equation**. The **solution of an equation** is defined as those values of the variables that make the equality be fulfilled.

>The **degree of an equation** is the value of the maximum exponent to which a variable is raised. Any equation of degree 1 is called a **linear equation**.

The basic rule for working with equations is that every time you make a change to one of the parts, you have to make the same change to the other part. For example:
$$ 3 - 2x = 6 + x $$
$$ 3 - 2x + 2x = 6 + x + 2x $$
$$ 3 = 6 + 3x $$
$$ 3 - 6 = 6 + 3x - 6 $$
$$ -3 = 3x $$
$$ \frac {-3} 3 = \frac {3x} 3 $$
$$ -1 = x $$

>There can also be equations that are **inequalities** (=/=, <, >, etc). They work in exactly the same way, except that if you multiply both sides of the equation by a negative number you have to "invert" the sign of the inequality. For example, < would become >.


```
Note: in the case of equations with roots, it is possible to obtain results that are not valid. To check this, simply substitute this value into the initial equation.
```

Given an equation $ax=b$:

- $\frac b a$ | The solution is $a/b$ if $a$ and $b$ are not zero.
- $\nexists$ | It has no solution if $a$ is zero and $b$ is non-zero.
- $\forall x \in \mathbb{R}$ | If $a$ and $b$ are zero, the solution is all the real numbers .


# Systems of equations

A **system of equations** is a group of two or more related equations. Generally, systems of equations can be solved, which means finding one or more values for the variables for which all of these equations are satisfied. 

>For example, given two straight lines in the form of a function, a system of equations can be formed where the solution will be the x and y values that are satisfied for both lines, i.e. their point of intersection. If two straight lines form a system that has no solution, it means that they are parallel.

There are 3 types of systems:

- **Incompatible**: no solution.
- **Determined compatible**: it has 1 solution per variable.
- **Indeterminate compatible**: it has infinite solutions.

___

The **systems of linear equations** are those where the maximum degree of the variables is 1.

A system of linear equations is said to be **homogeneous** if the independent term is zero in all the equations of the system. Every homogeneous system is compatible (has a solution): the **trivial solution** (where all the variables are zero).


# Type of solutions

An equation or system of equations can have solutions in multiple forms:

**Simple solutions:** 

- A number: $2x + 5 = 7 \rightarrow S = \{1\}$

- Several numbers: $x^2 - 3x + 2 = 0 \rightarrow S = \{1,2\}$

**Parametric solutions:** this means clearing one unknown and converting the rest into parameters.

- A solution with 1 parameter, i.e. a straight line (in this case the line $y = -x + 7$). 

$x + y = 7 \rightarrow S =\{(t, -t + 7), t \in \mathbb{R}\}$

- A 2-parameter solution, i.e. a plane: 

$x + 5y - z + 6 = 0 \rightarrow S = \{s,t,s + 5t + 6\,\ \ s,t \in \mathbb{R}\}$


# Algebraic solution

There are two methods for solving systems of equations. Using the following example: 

$$ y = x + 3 $$
$$ 2x - 3y = 10 $$

- **Substitution**: to clear a variable in one of the equations and substitute it in the other. 
$$ 2x - 3(x + 3) = 10 $$
$$ - x - 9 = 10 $$
$$ x = -19 $$
$$ y = -16 $$

- **Elimination**: eliminate a variable by manipulating one of the equations and subtracting it from the other. This is possible because we remember that both equations are worth the same on both sides of the equality, and we add the same on both sides of the equality of an equation.
$$ y = x + 3 $$
$$  -x + y = 3 $$
$$  -2x + 2y = 6 $$
$$ \{-2x + 2y = 6 \} + \{ 2x - 3y = 10\} $$
$$ 0 - y = 16 $$
$$ y = - 16 $$
$$ x = - 19 $$

- **Equalisation**: a variable is chosen and cleared from at least two equations to find its value.
$$ x = y - 3 $$
$$  x = \frac {10 - 3y} 2 $$

$$  y - 3 = \frac {10 - 3y} 2 $$
$$ 2y - 6 = 10 - 3y $$
$$ y = - 16 $$
$$ x = - 19 $$

# Matrix solutions

Matrices give us more power than [[#Algebraic solution|basic algebra]] when working with a lot of data. For example, if we had to solve a system of equations with 100 equations and 100 unknowns with algebra it would be a pain, but with matrices it is really simple.

Converting a system of equations to a matrix expression is simple. Being $A$ the matrix of coefficients, $X$ the matrix of variables and $B$ the matrix of independent terms, we can express the system as a product of matrices:
$$ A \cdot X = B $$
For example, given the following generic system, it could be expressed in matrix form as follows:
$$a_1 x_1 + b_1 x_2 = c_1 \ ||\ a_2 x_1 + b_2 x_2 = c_2$$
$$\begin{bmatrix} a_1 & b_1 \\ a_2 & b_2 \end{bmatrix} \cdot \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} c_1 \\ c_2 \end{bmatrix}$$

From here the **extended matrix** can be constructed:

$$A^*  = \begin{bmatrix} a_1 & b_1 & | & c_1 \\ a_2 & b_2 & | & c_1 \end{bmatrix}$$
# Rouchè-Fröbenius check

The Rouché-Fröbenius theorem is used to quickly find out the type of a system (incompatible, determinate compatible or indeterminate compatible).

>The theorem states that the necessary and sufficient condition for a system to be compatible (i.e. to have a solution), the **rank** of the coefficient matrix must be equal to the **rank** of the extended matrix.

There are the following options (where $n$ is the number of unknowns in the system):

1. $r(A) = n$ - determinate compatible system (1 solution).
2. $r(A) < n$ - indeterminate compatible system (infinite solutions).


# Gauss - Jordan solution

The solution by Gauss simply consists of **triangulating the matrix** through **elementary transformations**, so that only one unknown and one independent term remain on the bottom line. From there we will have the solution to the whole system.


# Inverse matrix solution

If a system of equations allows us to construct an invertible (and therefore square) matrix, we can use the inverse to solve the system. Knowing that the product by the inverse results in the identity ($A \cdot A^{-1} = I$), if we multiply the above formula by the inverse of the coefficient matrix, we obtain that:
$$A \cdot X = B \rightarrow A^{-1} \cdot A \cdot  X = A^{-1} \cdot  B  \rightarrow X = A^{-1} \cdot B $$
That is, the product of the matrix of independent terms by the inverse matrix of the coefficient matrix is the solution of the system. This solution consists of obtaining the inverse of the coefficient matrix and multiplying it by the matrix of independent terms, and we will have a matrix with all the solutions.


# Cramer solution

Cramer's rule is a very useful tool for solving systems of equations using determinants. The rule says that a system of equations is a **Cramer system** if it satisfies the following:

1. The matrix of the system is square (i.e. there is the same number of equations as unknowns).
2. The determinant of the coefficient matrix is not zero.

```
All Cramer systems are compatible determinate, and therefore the determinant of the coefficient matrix is non-zero, which means that it is invertible. 
```

Taking into account the matrix expression of a system of equations:

$$ A \cdot X = B \rightarrow \begin{bmatrix} a_{11} & a_{21} & ... & a_{i1} & ... & a_{n1} \\ a_{12} & a_{22} & ... & a_{i2}  & ... & a_{n2}  \\ ... & ... & ... & ... & ... & ... \\ a_{1i} & a_{2i} & ... & a_{ii} & ... & a_{ni} \\ ... & ... & ... & ... & ... & ... \\ a_{1n} & a_{2n} & ... & a_{in} & ... & a_{nn} \end{bmatrix} \cdot \begin{bmatrix} x_1 \\ x_2  \\ ...  \\ x_i \\ ...  \\ x_n \end{bmatrix} = \begin{bmatrix} b_1 \\ b_2  \\ ...  \\ b_i \\ ...  \\ b_n \end{bmatrix} $$

Given a Cramer system of $n$ equations and $n$ unknowns, its solution is a fraction of determinants, where:

- $|A|$ is the determinant of the coefficient matrix.
- $||\Delta_i|$ is the determinant of the matrix resulting from subtracting the column of the variable $x_i$ by the matrix of independent terms $B$ (which, remember, has only 1 column). 

$$x_i = \frac{|\Delta_i|}{|A|}$$
$$ \Delta_i = \begin{bmatrix} a_{11} & ... & b_{1} & ... & a_{n1}\\ a_{12} & ... & b_{2} & ... & a_{n2}\\ ... & ... & ... & ... & ...\\ a_{1n} & ... & b_{n} & ... & a_{nn}\\ \end{bmatrix} $$