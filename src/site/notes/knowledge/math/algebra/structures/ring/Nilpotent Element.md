---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/nilpotent-element/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 1.2: First examples and special classes of rings; Exercise 1.6.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — Exercise 16.7.27 (read at the mirror https://judsonbooks.org/aata-files/aata-html/; item numbers as there).

## Definition

> [!definition] Parameters
> - $R$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
> - $a$: an element of $R$.
> - $n$: a positive integer.

> [!definition] Nilpotent Element
> An element $a$ of a [[knowledge/math/algebra/structures/ring/Ring\|Ring]] $R$ is *nilpotent* if $a^n = 0$ for some positive integer $n$.
>
> `[Alu III.1.2]` `[Jud Ex 16.7.27]`

## Property

> [!proposition] Commuting nilpotents add — if $a, b$ are nilpotent and commute, $a + b$ is nilpotent
> If $a$ and $b$ are nilpotent in $R$ and $ab = ba$, then $a + b$ is also nilpotent.
>
> `[Alu III Ex 1.6]`

> [!proposition] Nilpotents form an ideal — in a commutative ring the nilpotent elements form an ideal
> If $R$ is a [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]], the set of nilpotent elements of $R$ is an [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] of $R$.
>
> `[Jud Ex 16.7.27]`

## Example

> [!example]
> In the [[knowledge/math/algebra/structures/ring/example/Matrix Ring\|Matrix Ring]] $M_2(\mathbb R)$, the matrix $\begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$ is nilpotent: its square is $0$.

## Related

### Constructions
- [[knowledge/math/algebra/structures/ring/ideal/Radical Ideal\|Radical Ideal]] — $\sqrt I$ is the preimage of the nilpotent elements of $R/I$
- [[knowledge/math/algebra/structures/ring/special ring/Reduced Ring\|Reduced Ring]] — no nilpotent element but $0$

### Prerequisites
- [[knowledge/math/algebra/structures/ring/Ring\|Ring]], [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]] (for the ideal of nilpotents).
