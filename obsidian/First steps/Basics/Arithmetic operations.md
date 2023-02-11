
The four basic operations of arithmetic are **addition**, **subtraction**, **multiplication** and **division**. These basic operations can be used to build more advanced things.


# Fractions and decimals

A fraction is a way of expressing a division. They two parts of a fraction are the **numerator** and the **denominator**. Only fractions with the same denominator can be added or subtracted (the operation only applies in the numerator). 
$$ \frac a c + \frac b c = \frac {a+b} c $$

Any fraction can be multiplied or divided by other fraction.

$$ \frac a b \cdot \frac c d = \frac {ac} {bd} $$
$$ \frac a b / \frac c d = \frac {ad} {bc} $$
 
A number consisting of a whole number and a fraction is called a **mixed number**. The value of that number is the sum of the whole number and the fraction. For example: 
 
$$ 1 \frac 1 2 =  1 + \frac 1 2 $$
  
An **improper fraction** is a fraction in which the numerator is greater than the denominator:
  
$$ \frac 3 2 $$

You can go from mixed number to improper fraction by adding the product of the integer part and the denominator to the numerator. Similarly, an improper fraction can be converted into a mixed number by dividing the numerator by the denominator. The quotient is the integer part, and the remainder is the new numerator.

$$ 1 \frac 1 2 = \frac 2 2 + \frac 1 2 = \frac 3 2 $$

**Decimal numbers** are numbers with a whole number part and a decimal part. All fractions can be expressed as decimal numbers, but not all decimal numbers as a fraction. In other words, there are **irrational** decimal numbers. The expression of a decimal number as a fraction is called the **generating fraction** of a decimal number. 

$$ \frac 3 4 =  0.75 $$
  
A **periodic decimal number** is a number with a repeating decimal part to infinity. They are expressed with a cap over the repeating decimal part.
$$ 0.33333333333333... = 0.\widehat{3} = \frac 1 3$$

Numbers with a non-repeating decimal part cannot be expressed as a fraction and are therefore **irrational**. An example is Pi $\pi$. 


# Powers
   
An **exponent** or **power** is a way of expressing a repeated product. The base indicates the starting number and the exponent the number of times it is multiplied by itself.
   
$$ 2^5 = 2 \cdot 2 \cdot 2 \cdot 2 \cdot 2 $$
Any number raised to 0 is 1.

$$ x^0 = 1 $$ 

We can only perform addition and subtraction operations with addends that have the variable of the same degree. Their factors are added or subtracted respectively.
   
$$ nx^a + mx^a + ox^b = (n + m) \cdot x^a + ox^b $$ 

When two powers have the same degree, the product and the quotient of these powers is the power of the product and the quotient.

$$ x^a \cdot y^a = (x \cdot y)^a $$
$$ \frac {x^a} {y^a} = (\frac {x} {y})^a $$

We can pass a power from the denominator to the numerator by inverting its sign. 
$$ \frac 1 {x^a} = x^{-a} $$
$$ \frac {a^{-2}} {b^{-2}} =(\frac {a} {b})^{-2} =  (\frac {b} {a})^2 $$

We can do product and quotient operations with factors that have different degrees. The degrees are added or subtracted respectively.

$$ nx^a \cdot mx^b = n \cdot m \cdot x^{a+b} $$
$$ \frac {nx^a} {mx^b} = \frac n m \cdot x^{a-b} $$

An exponent raised to another exponent results in multiplying their degrees.
$$ (x^a)^b = x^{a \cdot b} $$

# Factorials

The product of all the natural numbers before it is called the **factorial** of a number. It is expressed using exclamation mark notation.
$$ x! $$
$$ 4! = 1 \cdot 2 \cdot 3 \cdot 4 = 24 $$
# Roots

The **radicals** or **roots** are the inverse operation of powers. That is: which number multiplied by itself n times gives the specified number. The number inside the root is called the **radicand**. The small number above the root is called the **index**. If there is no index represented, it is assumed to be 2.
$$ 2^2 = 4 \rightarrow \sqrt{4} = 2 $$
$$ 2^3 = 8 \rightarrow \sqrt[3]{8} = 2 $$

>Note: even roots always have 2 possible roots (one positive and one negative), since a negative number multiplied by itself an even number of times gives a positive number.


Roots can be expressed as a power as a denominator.
$$ \sqrt[3]{5^2} = 5^{\frac 2 3} $$

Roots can only be added to or subtracted from other roots of the same degree and radical as themselves.  
$$ 2\sqrt{3} + 5\sqrt{3} = 7\sqrt{3} $$

The product or division of roots of the same degree is equal to the root of the product or division.
$$ \sqrt{3} \cdot \sqrt{5} = \sqrt{3 \cdot 5} = \sqrt{15} $$
$$ \frac {\sqrt{3}} {\sqrt{5}} = \sqrt{\frac 3 5} $$

A root of a root results in a root where the indices are multiplied.
$$ \sqrt[3]{\sqrt[5]{2}} = \sqrt[15]{2} $$

This means that we can sometimes refactor roots in order to operate on them.
$$ \sqrt{2} + \sqrt{8} = \sqrt{2} + \sqrt{2 \cdot 4} = \sqrt{2} + \sqrt{2} \cdot \sqrt{4} = \sqrt{2} + 2\sqrt{2} = 3\sqrt{2} $$

The product or division of roots of different degrees can be better understood by expressing radicals as powers:
$$ \sqrt[3]{5} \cdot \sqrt{2} = 5^{\frac 1 3} \cdot 2^{\frac 1 2} = (5 \cdot 2)^{\frac 1 3 + \frac 1 2} = 10^{\frac 5 6} = \sqrt[6]{10^5}$$ 

The conversion of a fraction with a root in the denominator to an equivalent fraction where there are no roots in the denominator is called **rationalisation**. 

>In the case of monomials it is simple; just multiply the fraction by another unit fraction where both the denominator and the numerator are the root.

$$ \frac 1 {\sqrt 2} = \frac 1 {\sqrt 2} \cdot \frac {\sqrt 2} {\sqrt 2} = \frac {\sqrt 2} 2 $$

>In the case of binomials, the third of the **notable identities** can be used to eliminate the root.

$$ \frac 1 {1 + \sqrt 2} = \frac 1 {1 + \sqrt 2} \cdot \frac {1 - \sqrt 2} {1 - \sqrt 2} = \frac {1 - \sqrt 2} {1 - 2} $$


# Logarithms

Logarithms are similar to roots, but have the exponent as a variable instead of the base. That is: given two constants `a` and `b`, to which number must `a` be raised to give `b`.:
$$ \log_{3} 9 = 2 $$
Any logarithm of base 1 is equal to 0 (because any number raised to 0 is equal to 1).
$$ \log_{a} 1 = 0 $$
 
Any logarithm with the same base as the result is always 1, because any number raised to one is itself.
$$ \log_{a} a = 1 $$
 
A logarithm of the same degree as the base is always equal to the exponent.
$$ \log_{a} a^n = n $$
 
The logarithm of a power is equal to the product of the degree of the power and the logarithm, provided that the argument is greater than 0. The same applies to roots if they are expressed as a power.
$$ \log_{a} b^n = n \cdot \log_{a} b \iff b > 0 $$
$$ \log_{a} (\sqrt[n]{b}) = \log_{a} (b^{\frac 1 n}) = \frac 1 n \cdot \log_{a} b \iff b > 0 $$
  
A logarithm of the product is equal to the sum of logarithms if all factors are positive.
  
$$ \log_{a} (b \cdot c) = \log_{a} b + \log_{a} c \iff b > 0, c > 0 $$
  
A quotient of logarithms is equal to the subtraction of logarithms if all factors are positive.
  
$$ \log_{a} (\frac b c) = \log_{a} b - \log_{a} c \iff b > 0, c > 0 $$
  
The **neperian logarithm** or **natural logarithm** is defined as the **number e** (2.7128...).
  
$$ \ln(b) = \log_{e} b $$
  
By definition, a positive base logarithm can only result in a positive number. That is, a positive number raised to any number will always be positive.
$$ \log_{a} b $$
$$ a > 0 \iff b > 0 $$
 
You can change the base of any logarithm using the following formula, where c can be any number:
 
$$ \log_{a} b = \frac {\log_c b} {\log_c a} $$

>Logarithms cannot be multiplied and divided directly. At most, a change of base can be made to try to simplify them. In the case of logarithmic equations, you have to try to isolate the variable and then calculate the numerical result with a calculator.


# Complex numbers

The set of imaginary numbers is based on the root number of minus one, called `i` or imaginary unit, and allows us to work with negative roots. An **imaginary number** is a number that has only one imaginary part.

$$ i = \sqrt{-1} $$
$$ i^2 = -1 $$
$$ i^4 = 1 $$
$$ i^n = i^{4m+k} = i^{4m} \cdot i^k = i^k $$

For instance:

$$ i^{13} = i^{4*3+1} = i^1 = i $$

They work in a similar way to variables in algebraic expressions. We can take any negative root and turn it into an imaginary unit product.

$$ \sqrt{-9} = \sqrt{9} \cdot \sqrt{-1} = 3i $$

Numbers composed of a real part and an imaginary part are called **complex numbers**. They can be expressed in **Cartesian form** (two real numbers, where the second is the factor of the imaginary part) or in **binomial form**.

$$ \mathbb{Z} = (a,b);\ a \in \mathbb{R}, b \in \mathbb{R} = a + bi $$

>Complex numbers can be operated with the real part on one side and the imaginary part on the other.

The **module** of a complex number is the distance from the origin to its representation in Cartesian space (the x-axis being the real numbers and the y-axis the imaginary numbers). That is to say: 

$$ m(a + bi) = \sqrt{a^2 + b^2} $$

This has several properties:

$$ m(a_1 + b_1i) + m(a_2 + b_2i) = m(a_1 + a_2 + b_1i + b_2i) $$
$$ m(a_1  b_1i) \cdot m(a_2 + b_2i) = m((a_1 + b_1i) \cdot (a_2 + b_2i)) $$

>A complex number with the sign of the imaginary part inverted is called a **conjugate** of a complex number.