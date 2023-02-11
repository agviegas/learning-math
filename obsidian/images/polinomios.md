# Introducción
Un **polinomio** es una expresión consistente en la suma de múltiples términos que multiplican a una variable. Es un caso particular de las [[Algebra concepts |expresiones algebraicas]]. 

Los polinomios se expresan con una letra mayúscula (generalmente P) y las variables de las que depende entre paréntesis. Por ejemplo:

$$ P(x) = 2x^4 + 3x + 2 $$

Para que una expresión algebraica se considere un polinomio, debe cumplir las siguientes condiciones:

- Los exponentes tienen que ser números enteros positivos.
- Debe tener un número finito de constantes y de variables.

$$ P(x) = a_m\ x^m\ +\ a_{m-1}\ x^{m-1}\ +\ ...\ +\ a_1\ x^1\ +\ a_0$$

$$m \in \mathbb{Z}: x > 0$$

Por ejemplo, una expresión algebraica que tenga $x^{\frac12}$, o lo que es lo mismo, $\sqrt{x}$, no se considera un polinomio.

___
- Se denomina monomio a cada uno de los términos algebraicos de un polinomio.

- Se denomina binomio a un polinomio compuesto por dos monomios.

- Se denomina término independiente al término algebraico sin variable.
___

Siguiendo las normas de la [[aritmética]], solo pueden hacerse operaciones de suma y resta con términos algebraicos equivalentes. Por ejemplo:

$$ P(x) = 2x^2 + 3x^2 + 4x + 5y = 5x^2 + 4x + 5y $$

En cambio, se pueden efectuar productos y cocientes independientemente de la variable o grado. En este caso se suman o restan los exponentes y se multiplican las bases y los coeficientes respectivamente.

$$ P(x) = 2x^2 \cdot 3x^2 \cdot 4x \cdot 5y = 120x^5 y $$

Ojo, si multiplicamos o dividimos polinomios entre sí se cumple la **propiedad distributiva**.

$$ P(x) = (x^2 + 1)(x - 5) = x^3 - 5x^2 + x - 5 $$

$$ P(x) = \frac {x + 1} {x - 1} = \frac x {x - 1} + \frac 1 {x - 1} $$

# Factorización

Se denomina **factorizar un polinomio** a descomponerlo en un producto de sus factores.  Es lo equivalente a factorizar un número a factores primos. Cada uno de los factores de un polinomio suele tener la siguiente estructura, siendo $x$ la variable y $a$ una constante:

$$ (x - a) $$

Se denomina **raíces** de un polinomio a aquellos valores que si se sustituyen en x igualan el polinomio a cero. Este concepto es importante para poder factorizar polinomios.

```
Al igual que con los números sencillos, la factorización se usa, por ejemplo, si queremos sumar o restar fracciones cuyos denominadores son polinomios. Podemos encontrar el mínimo común múltiplo usando sus factores.
```

```
Si representamos un polinomio en 2d, las raíces son los puntos donde la curva intersecta con el eje X (y = 0).
```

Para polinomios cuadráticos se puede usar la [fórmula cuadrática](https://es.wikipedia.org/wiki/Ecuaci%C3%B3n_de_segundo_grado). Dado un polinomio:

$$ P(x) = ax^2 + bx + c $$

Sus raíces son iguales a:

$$ \frac {-b \pm \sqrt{b^2 - 4ac}}{2a} $$

El signo más-menos indica que hay dos raíces: una resolviendo la fórmula con más y otra con menos. 

Una vez encontradas las raíces del polinomio (ej. r1, r2) se puede factorizar el polinomio:

$$ P(x) = (x - r_1)(x - r_2) $$

Lo que hay dentro de la raíz se llama **discriminante**. Hay 3 escenarios:

- Es positivo: las 2 raíces son reales y diferentes.
- Es cero: las 2 raíces son reales e iguales.
- Es negativo: las dos raíces son imaginarias.

Las 2 raíces ($r_1$, $r_2$) de un polinomio cuadrático cumplen lo siguiente (siendo a, b, c los factores de los 3 sumandos que componen el polinomio):

$$ r_1 + r_2 = \frac{-b} a $$
$$ r_1 \cdot r_2 = \frac c a $$


Para encontrar las raíces de un polinomio de mayor grado se puede usar el método de [Ruffini](https://www.youtube.com/watch?v=X__hA6i6Ykk). Por ejemplo:

$$ P(x) = -x^4 + 10^2 - 9 $$

Si las raíces (por Ruffini) son 1, -1, 3 y -3, los factores del polinomio se definen como binomios donde el término independiente son las raíces cambiadas de signo:

$$ P(x) = (x - 1)(x + 1)(x - 3)(x + 3) $$

Algunos polinomios se pueden factorizar fácilmente usando [[identidades notables]].

$$ P(x) = 9x^2 - 16 = (3x - 4)(3x + 4) $$


