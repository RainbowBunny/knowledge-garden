---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/field/field/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 1.2: First examples and special classes of rings.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ (numbering as on the LibreTexts / AIM mirrors).
- `[Ax]` — S. Axler, _Linear Algebra Done Right_ (4th ed., open access): https://linear.axler.net/
- `[Wiki]` — Wikipedia, _Field trace_ (§ Finite fields) and _Euler's formula_: https://en.wikipedia.org/wiki/Field_trace · https://en.wikipedia.org/wiki/Euler%27s_formula
- `[Isr02]` — R. Israel, _Constant Coefficients: Complex Roots_ (UBC Math 215 notes, 2002): https://personal.math.ubc.ca/~israel/m215/cococom/cococom.html

## Definition

> [!definition] Field
> Extends:: [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]].
>
> ---
> A field is a [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]] with $1 \neq 0$ in which every nonzero element has a multiplicative [[knowledge/math/property/operation/Inverse Element\|inverse]] (or being a [[knowledge/math/algebra/structures/ring/Ring#Unit\|Unit]]).
>
> `[Alu III.1.2]` `[Jud §16.2]`

## Structure

### Characteristic

Specializes [[knowledge/math/algebra/structures/ring/Ring#Characteristic\|Characteristic]] — a field is a ring.

> [!definition] Parameters
> - $R$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].

> [!definition] Characteristic (elementwise form)
> The characteristic of a ring $R$ is the least positive integer $n$ s.t $nr = 0$ for all $r \in R$. If no such integer exists, the characteristic of $R$ is $0$.
>
> `[Jud §16.2]`

> [!theorem] Characteristic of an integral domain — it is either prime or zero
> The characteristic of an [[knowledge/math/algebra/structures/ring/special ring/Integral Domain\|Integral Domain]] is either prime or zero; in particular, so is the characteristic of a field.
>
> `[Jud Thm 16.19]`

## Property

> [!proposition] Fields are integral domains — a field has no zero divisors
> Every field is an [[knowledge/math/algebra/structures/ring/special ring/Integral Domain\|Integral Domain]].
>
> `[Alu III.1.2]`

### Arithmetic in a field

Consequences of the field axioms. The rows under *Addition* hold in every [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]], those under *Addition and multiplication* in every [[knowledge/math/algebra/structures/ring/Ring\|Ring]].

#### Addition

| Property                      | Description                                                                                                                                                                         | Hypothesis |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| Cancellation Law for Addition | If $a + b = a + c$, then $b = c$                                                                                                                                                    |            |
| Possibility of Subtraction    | Given $a$ and $b$, there is exactly one $x$ such that $a + x = b$. This $x$ is denoted by $b - a$. In particular, $0 - a$ is written simply $-a$ and is called the negative of $a$. |            |
|                               | $b - a = b + (-a)$                                                                                                                                                                  |            |
|                               | $-(-a) = a$                                                                                                                                                                         |            |
|                               | $-0 = 0$                                                                                                                                                                            |            |
|                               | $-(a + b) = -a - b$                                                                                                                                                                 |            |
|                               | $-(a - b) = -a + b$                                                                                                                                                                 |            |
|                               | $(a - b) + (b - c) = a - c$                                                                                                                                                         |            |

#### Addition and multiplication

| Property | Description                 | Hypothesis |
| -------- | --------------------------- | ---------- |
|          | $a(b - c) = ab - ac$        |            |
|          | $0 \cdot a = a \cdot 0 = 0$ |            |
|          | $(-a)b = -(ab)$             |            |
|          | $(-a)(-b) = ab$             |            |

#### Multiplication

| Property                            | Description                                                                                                                                                                                                                       | Hypothesis                 |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| Cancellation Law for Multiplication | If $ab = ac$, then $b = c$                                                                                                                                                                                                        | $a \neq 0$                 |
| Possibility of Division             | Given $a$ and $b$, there is exactly one $x$ such that $ax = b$. This $x$ is denoted by $b / a$ or $\frac{b}{a}$ and is called the quotient of $b$ and $a$. In particular, $1/a$ is also written $a^{-1}$ and is called the reciprocal of $a$. | $a \neq 0$                 |
|                                     | $b / a = b \cdot a^{-1}$                                                                                                                                                                                                          | $a \neq 0$                 |
|                                     | $(a^{-1})^{-1} = a$                                                                                                                                                                                                               | $a \neq 0$                 |
|                                     | If $ab = 0$, then $a = 0$ or $b = 0$                                                                                                                                                                                              |                            |
|                                     | $0$ has no reciprocal                                                                                                                                                                                                             |                            |
|                                     | $(ab)^{-1} = a^{-1} b^{-1}$                                                                                                                                                                                                       | $a \neq 0$ and $b \neq 0$  |

#### Fractions

| Property | Description                        | Hypothesis                            |
| -------- | ---------------------------------- | ------------------------------------- |
|          | $(a/b) + (c/d) = (ad + bc)/(bd)$   | $b \neq 0$ and $d \neq 0$             |
|          | $(a/b) - (c/d) = (ad - bc)/(bd)$   | $b \neq 0$ and $d \neq 0$             |
|          | $(a/b)/(c/d) = (ad)/(bc)$          | $b \neq 0$, $c \neq 0$ and $d \neq 0$ |
|          | $-(a/b) = (-a)/b = a/(-b)$         | $b \neq 0$                            |

## Example

### Finite Fields

> [!theorem] Integers modulo $m$ — $\mathbb Z_m$ is a field iff $m$ is prime
> $\mathbb Z_m$ is a field if and only if $m$ is a prime.
>
> `[Jud Ex 16.17]`

> [!theorem] Existence and uniqueness of finite fields — exactly one field of each prime-power size
> Let $p$ be a prime and $\mathbb F_p$ the finite field with $p$ elements.
> 1. For every $d \geq 1$ there exists an irreducible polynomial $m \in \mathbb F_p[x]$ of degree $d$.
> 2. For every $d \geq 1$ there exists a finite field with $p^d$ elements.
> 3. If $\mathbb F$ and $\mathbb F'$ are finite fields with the same number of elements, then $\mathbb F$ and $\mathbb F'$ are isomorphic.
>
> `[Jud Thm 22.6]` (items 2 and 3)

> [!theorem] Primitive root theorem — the multiplicative group of a finite field is cyclic
> Let $\mathbb F$ be a finite field having $q$ elements. Then $\mathbb F$ has a primitive root, i.e., there is an element $g \in \mathbb F$ such that
> $$\mathbb F^* = \{1, g, g^2, g^3, \dots, g^{q - 2}\}.$$
>
> `[Jud Cor 22.11]`

> [!example]
> If $p \equiv 3 \pmod 4$, then the field with $p^2$ elements looks like
> $$\mathbb F_{p^2} = \{a + bi : a, b \in \mathbb F_p\},$$
> where $i$ satisfies $i^2 = -1$.

> [!proposition] Characteristic of a finite field — a prime $p$, and the field has $p^n$ elements
> Based on the previous definition of characteristic [[knowledge/math/algebra/structures/field/Field#Characteristic\|Field#Characteristic]], one can derive the characteristic for finite field $\mathbb{F}_p$ is $p$. More generally:
> - a finite field has characteristic $p$ for some prime $p$;
> - a finite field of characteristic $p$ has $p^n$ elements for some $n \in \mathbb N$.
>
> `[Jud Ex 16.17]` `[Jud Prop 22.1]` `[Jud Prop 22.2]`

> [!lemma] Every element is a root of $x^q - x$ — $\beta^q = \beta$ in a field with $q$ elements
> For every element $\beta$ of a finite field $\mathbb F$ with $q$ elements, we have $\beta^q = \beta$.
>
> `[Jud Cor 6.11]` applied to $\mathbb F^*$; `[Jud §22.1]` (proof of Thm 22.6)

> [!corollary] Subfield test — $\beta \in F$ iff $\beta^q = \beta$
> Let $F$ be a subfield of $E$ with $|F| = q$. Then an element $\beta$ of $E$ lies in $F$ if and only if $\beta^q = \beta$.
>
> `[cf. Jud Thm 22.7]`

> [!definition] Parameters
> - $p$: a prime.
> - $d \geq 1$: an integer.

> [!definition] Galois Fields
> We write $\mathbb F_{p^d}$ for a field with $p^d$ elements. We know that any two fields with $p^d$ elements are essentially the same. These fields are also sometimes called **Galois fields** and denoted by $\text{GF}(p^d)$.
>
> `[Jud §22.1]`

#### Order of an element

Specializes [[knowledge/math/algebra/structures/group/Group Order\|Group Order]] — the order of $\alpha$ as an element of the multiplicative group $\mathbb F_q^*$.

> [!definition] Parameters
> - $q$: a prime power.
> - $\alpha \in \mathbb F_q^*$: a nonzero element.

> [!definition] Order
> The **order** of a nonzero element $\alpha \in \mathbb F_q$, denoted by $\text{ord}(\alpha)$, is the smallest positive integer $k$ such that $\alpha^k = 1$.
>
> `[Jud §4.1]`

> [!lemma] Orders in $\mathbb F_q^*$ — they divide $q - 1$, and multiply when coprime
> 1. The order $\text{ord}(\alpha)$ divides $q - 1$ for every $\alpha \in \mathbb F_q^*$.
> 2. For two nonzero elements $\alpha, \beta \in \mathbb F_q^*$, if $\gcd(\text{ord}(\alpha), \text{ord}(\beta)) = 1$, then $\text{ord}(\alpha \beta) = \text{ord}(\alpha) \times \text{ord}(\beta)$.
>
> `[Jud Cor 6.11]` (item 1); item 2 holds for commuting elements of any group, see [[knowledge/math/algebra/structures/group/Group Order#Commute Element\|Group Order#Commute Element]].

#### Extension Field

> [!definition] Parameters
> - $q$: a prime power.
> - $m \geq 1$: an integer.
> - $x \in \mathbb F_{q^m}$.

> [!definition] Trace Function
> The trace of $\mathbb F_{q^m}$ over $\mathbb F_q$ is the map $\text{Tr}: \mathbb F_{q^m} \rightarrow \mathbb F_q$ given by
> $$\text{Tr}(x) = \sum_{l = 0}^{m - 1} x^{q^l}.$$
>
> `[Wiki]` (Field trace: the sum of the Galois conjugates $x, x^q, \dots, x^{q^{m-1}}$)

### Complex Field

> [!definition] Parameters
> - $a, b \in$ [[knowledge/math/calculus/Real Number\|$\mathbb R$]].

> [!definition] Complex Number
> A **complex number** is an ordered pair $(a, b)$, where $a, b \in \mathbb R$, but we will write this as $a + bi$ where $i^2 = -1$. The set of all complex numbers is denoted by $\mathbb C$:
> $$\mathbb C = \{a + bi : a, b \in \mathbb R\}.$$
>
> `[Ax 1.1]`

> [!definition] Parameters
> - $a, b, c, d \in \mathbb R$.

> [!definition] Addition and multiplication on $\mathbb C$
> Addition and multiplication on $\mathbb C$ are defined by:
> $$\begin{align}
> (a + bi) + (c + di) &= (a + c) + (b + d) i \\
> (a + bi)(c + di) &= (ac - bd) + (ad + bc)i
> \end{align}$$
>
> `[Ax 1.1]`

> [!definition] Parameters
> - $a, b \in \mathbb R$.
> - $z = a + bi \in \mathbb C$.

> [!definition] Real Part, Imaginary Part
> Suppose $z = a + bi$, where $a$ and $b$ are real numbers. Then $a$ is called the **real part** of $z$, denoted $\text{Re } z$, and $b$ is called the **imaginary part** of $z$, denoted $\text{Im } z$. Thus for every complex number $z$, we have
> $$z = \text{Re } z + (\text{Im } z) i.$$
>
> `[Jud §4.2]`

> [!definition] Parameters
> - $z \in \mathbb C$.

> [!definition] Complex Conjugate
> The **complex conjugate** of $z \in \mathbb C$, denoted by $\overline z$, is defined by
> $$\overline z = \text{Re } z - (\text{Im } z) i.$$
>
> `[Jud §4.2]`

> [!definition] Parameters
> - $(x, y) \in \mathbb R^2$ with $(x, y) \neq (0, 0)$.
> - $r > 0$, $\theta \in \mathbb R$: its polar coordinates.

> [!definition] Polar Coordinates
> If point $(x, y) \neq (0, 0)$, we can express $x$ and $y$ in polar coordinates,
> $$x = r \cos \theta$$
> $$y = r \sin \theta$$
> and we obtain
> $$x + iy = r(\cos \theta + i \sin \theta).$$
> And thus we have the **modulus** or **absolute value**
> $$|x + iy| = \sqrt{x^2 + y^2}.$$
> And the polar angle $\theta$ is the **argument** of $x + iy$.
>
> `[Jud §4.2]`

> [!proposition] Real Möbius maps — for $ad - bc > 0$, $w$ and $z$ have imaginary parts of the same sign
> Let $w = (az + b) / (cz + d)$, where $a, b, c$ and $d$ are real and $cz + d \neq 0$. Then,
> $$w - \overline{w} = (ad - bc)(z - \overline{z})/|cz + d|^2.$$
> If $ad - bc > 0$, then the imaginary parts of $z$ and $w$ have the same sign.
>
> `[no source checked]` — verified by direct computation.

#### Complex Exponentials

> [!definition] Parameters
> - $x, y \in \mathbb R$.
> - $z = x + iy \in \mathbb C$.

> [!definition] Complex Exponential
> If $z = x + iy$, we define $e^z$ to be the complex number given by the equation
> $$e^z = e^x (\cos y + i \sin y).$$
>
> `[Wiki]` (Euler's formula)

> [!theorem] Exponential law — $e^a e^b = e^{a + b}$ for complex $a, b$
> If $a$ and $b$ are complex numbers, we have
> $$e^a e^b = e^{a + b}.$$
>
> `[Wiki]` (Euler's formula)

> [!theorem] Polar form — every nonzero complex number is $re^{i\theta}$
> Every complex number $z \neq 0$ can be expressed in the form
> $$z = r e^{i \theta}$$
> where $r = |z|$ and $\theta = \text{arg}(z) + 2n \pi$, $n$ being any integer. This representation is called the polar form of $z$.
>
> `[Wiki]` (Euler's formula) `[Jud §4.2]`

#### Complex-valued Functions

> [!definition] Parameters
> - $u, v$: real-valued functions on an interval of $\mathbb R$.
> - $f = u + iv$.

> [!definition] Derivative, Integral of Complex-valued Function
> If $f = u + iv$, we say $f$ is continuous at a point if both $u$ and $v$ are continuous at that point. The derivative of $f$ is defined by the equation
> $$f'(x) = u'(x) + iv'(x)$$
> whenever both derivatives $u'(x)$ and $v'(x)$ exist. Similarly, we define the integral of $f$ by the equation
> $$\int_a^b f(x) dx = \int_a^b u(x) dx + i \int_a^b v(x) dx$$
> whenever both integrals on the right exist.
>
> `[no source checked]`

> [!theorem] Derivative of $e^{tx}$ — it is $te^{tx}$
> If $f(x) = e^{tx}$ for all real $x$ and a fixed complex $t$, then $f'(x) = te^{tx}$.
>
> `[cf. Wiki]` (Euler's formula: the case $t = i$)

> [!theorem] Characteristic equation — $e^{tx}$ gives real solutions of $y'' + ay' + by = 0$ iff $t^2 + at + b = 0$
> Consider the differential equation
> $$y'' + ay' + by = 0,$$
> where $a$ and $b$ are real constants. The real and imaginary parts of the function $f$ defined on $(-\infty, +\infty)$ by the equation $f(x) = e^{tx}$ are solutions of the differential equation if and only if $t$ is a root of the characteristic equation
> $$t^2 + at + b = 0.$$
>
> `[Isr02]`

#### Complex Formula

Sources: `[Wiki]` (Euler's formula) for the first two rows, `[Jud Thm 4.22]` for DeMoivre's Theorem.

| Condition                                        | Property           | Description                                                       |
| ------------------------------------------------ | ------------------ | ----------------------------------------------------------------- |
| If $\theta$ is real                              |                    | $\cos \theta = \frac{e^{i\theta} + e^{-i\theta}}{2}$              |
| If $\theta$ is real                              |                    | $\sin \theta = \frac{e^{i \theta} - e^{-i\theta}}{2i}$            |
| If $\theta$ is real and $n = 1, 2, \dots$        | DeMoivre's Theorem | $(\cos \theta + i \sin \theta)^n = \cos n\theta + i \sin n\theta$ |

## Related

### Siblings
- [[knowledge/math/algebra/structures/ring/special ring/Division Ring\|Division Ring]] — drops commutativity
- [[knowledge/math/algebra/structures/ring/special ring/Integral Domain\|Integral Domain]] — every field is one; a finite integral domain is a field `[Jud Thm 16.16]`

### Constructions
- [[knowledge/math/algebra/structures/ring/ideal/Maximal Ideal\|Maximal Ideal]] — $R/I$ is a field exactly when $I$ is maximal
- [[knowledge/math/algebra/structures/ring/subring/Ring Center\|Ring Center]] — the center of a division ring is a field
- [[knowledge/math/algebra/structures/polynomial/Polynomial Ring\|Polynomial Ring]] — $F[x]$
- [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]] — modules over a field
- [[knowledge/math/algebra/linear algebra/Vector Spaces Over Finite Fields\|Vector Spaces Over Finite Fields]] — over $\mathbb F_q$
- [[knowledge/math/algebra/structures/elliptic curve/Elliptic Curves over Finite Fields\|Elliptic Curves over Finite Fields]] — curves over $\mathbb F_q$

### Prerequisites
- [[knowledge/math/algebra/structures/ring/Ring#Characteristic\|Ring#Characteristic]] — the origin of the characteristic
- [[knowledge/math/algebra/structures/group/Group Order\|Group Order]] — the origin of the element order
