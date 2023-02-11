
A **polynomial** is an expression consisting of the sum of multiple terms multiplying a variable. It is a particular case of [[Algebra concepts |algebraic expressions]]. 

Polynomials are expressed with a capital letter (usually P) and the variables on which it depends in brackets. For example:

$$ P(x) = 2x^4 + 3x + 2 $$

For an algebraic expression to be considered a polynomial, it must meet the following conditions:

- The exponents must be positive integers.
- It must have a finite number of constants and variables.

$$ P(x) = a_m\ x^m\ +\ a_{m-1}\ x^{m-1}\ +\ ...\ +\ a_1\ x^1\ +\ a_0$$

$$m \in \mathbb{Z}: x > 0$$

For example, an algebraic expression with $x^{\frac12}$, or $\sqrt{x}$, is not considered a polynomial.

___
- Each of the algebraic terms of a polynomial is called a monomial.

- A polynomial composed of two monomials is called a binomial.

- An independent term is an algebraic term without a variable.
___

Following the rules of [[Arithmetic operations|arithmetic]], only addition and subtraction operations can be performed with equivalent algebraic terms. For example:

$$ P(x) = 2x^2 + 3x^2 + 4x + 5y = 5x^2 + 4x + 5y $$

On the other hand, products and quotients can be carried out independently of the variable or degree. In this case, the exponents are added or subtracted and the bases and coefficients are multiplied respectively.

$$ P(x) = 2x^2 \cdot 3x^2 \cdot 4x \cdot 5y = 120x^5 y $$

Note that if we multiply or divide polynomials with each other, the **distributive property** is fulfilled.

$$ P(x) = (x^2 + 1)(x - 5) = x^3 - 5x^2 + x - 5 $$

$$ P(x) = \frac {x + 1} {x - 1} = \frac x {x - 1} + \frac 1 {x - 1} $$

# Notable identities

Notable identities are formulas used to operate with binomials. There are 3 of them:

$$ (a + b)^2 = a^2 + b^2 + a \cdot b $$
$$ (a - b)^2 = a^2 + b^2 - a \cdot b $$
$$ (a - b) \cdot (a + b) = a^2 - b^2 $$

# Factorization

Factoring a polynomial into a product of its factors is called **factorising a polynomial**.  It is the equivalent of factoring a number into prime factors. Each of the factors of a polynomial usually has the following structure, with $x$ being the variable and $a$ a constant:

$$ (x - a) $$

The **roots** of a polynomial are those values which, when substituted into x, make the polynomial equal to zero. This concept is important for factoring polynomials.

```
As with simple numbers, factorisation is used, for example, if we want to add or subtract fractions whose denominators are polynomials. We can find the least common multiple by using their factors.
```

```
If we represent a polynomial in 2d, the roots are the points where the curve intersects the x-axis (y = 0).
```

For quadratic polynomials the **quadratic formula** can be used. Given a polynomial:

$$ P(x) = ax^2 + bx + c $$

Its roots are equal to:

$$ \frac {-b \pm \sqrt{b^2 - 4ac}}{2a} $$

The plus-minus sign indicates that there are two roots: one solving the formula with plus and one with minus. 

Once the roots of the polynomial (e.g. r1, r2) have been found, the polynomial can be factored:

$$ P(x) = (x - r_1)(x - r_2) $$

What is inside the root is called **discriminant**. There are 3 scenarios:

- It is positive: the 2 roots are real and different.
- It is zero: the 2 roots are real and equal.
- It is negative: the 2 roots are imaginary.

The 2 roots ($r_1$, $r_2$) of a quadratic polynomial satisfy the following (a, b, c being the factors of the 3 summands that make up the polynomial):

$$ r_1 + r_2 = \frac{-b} a $$
$$ r_1 \cdot r_2 = \frac c a $$


To find the roots of a polynomial of higher degree you can use the [Ruffini](https://en.wikipedia.org/wiki/Ruffini%27s_rule) method. For example:

$$ P(x) = -x^4 + 10^2 - 9 $$

If the roots (by Ruffini) are 1, -1, 3 and -3, the factors of the polynomial are defined as binomials where the independent term is the sign-changed roots:

$$ P(x) = (x - 1)(x + 1)(x - 3)(x + 3) $$

Some polynomials can be easily factored using [[#Notable identities|notable identitites]].

$$ P(x) = 9x^2 - 16 = (3x - 4)(3x + 4) $$
