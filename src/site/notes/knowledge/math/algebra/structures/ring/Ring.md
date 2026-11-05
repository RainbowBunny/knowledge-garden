---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/ring/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 1.1: Definitions; Section 1.2: First examples and special classes of rings; Section 3.2: Quotients.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — §16.1 Rings; §16.2 Integral Domains and Fields; Exercise 16.7.35 (read at the mirror https://judsonbooks.org/aata-files/aata-html/; item numbers as there).

## Definition

> [!definition] Parameters
> - $R$: a [[knowledge/math/set theory/Set\|Set]].
> - $+$: a [[knowledge/math/set theory/operation/Binary Operation\|Binary Operation]] on $R$ (addition).
> - $*$: a [[knowledge/math/set theory/operation/Binary Operation\|Binary Operation]] on $R$ (multiplication).

> [!definition] Ring
> A **ring** is a set $R$ that has two [[knowledge/math/set theory/operation/Binary Operation\|Binary Operation]] $+, *$:
> - $(R, +)$ is an [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]].
> - $(R, *)$ is a [[knowledge/math/algebra/structures/Monoid\|Monoid]].
> - $+$ and $*$ satisfies [[knowledge/math/property/operation/Distributivity\|Distributivity]].
>
> `[Alu III.1.1]`

> [!remark] Convention: a ring has $1$
> In this vault (following `[Alu]`) a ring has a multiplicative identity $1$, since $(R, *)$ is a monoid, and $0 = 1$ is allowed: that is the [[knowledge/math/algebra/structures/ring/example/Zero Ring\|Zero Ring]].
> `[Jud §16.1]` asks only that $*$ be associative. There a *ring with identity* (*unity*) is one with an element $1 \neq 0$ such that $1a = a1 = a$ for all $a$. Statements quoted from `[Jud]` are read with this difference in mind.

## Structure

### Zero Divisor

> [!definition] Parameters
> - $R$: a ring.
> - $a$: an element of $R$.
> - $b$: an element of $R$.

> [!definition] Zero Divisor
> An element $a \in R$ is a **left-zero-divisor** if there exist elements $b \neq 0$ in $R$ for which $ab = 0$.
> Similarly, an element $b \in R$ is a **right-zero-divisor** if there exist elements $a \neq 0$ for which $ab = 0$.
>
> `[Alu III.1.2]`

> [!remark] Zero divisors in `[Jud]`
> `[Jud §16.1]` defines a zero divisor only in a commutative ring, and only for a *nonzero* element $a$. With the definition above, $0$ is a left- and right-zero-divisor in every nonzero ring (take $b = 1$).

> [!proposition] Zero-divisors and injectivity — $a$ is not a left-zero-divisor iff $x \mapsto ax$ is injective
> In a ring $R$, $a \in R$ is not a left-(right-)zero-divisor if and only if left (resp., right) multiplication by $a$ is an [[knowledge/math/property/map/Injection\|Injection]] on $R$.
>
> `[Alu III.1.2]`

### Unit

> [!definition] Parameters
> - $R$: a ring.
> - $u$: an element of $R$.
> - $v$: an element of $R$.

> [!definition] Unit
> An element $u$ of a ring $R$ is a (two-sided) unit iff
> - $\exists v \in R: uv = 1$ (left-unit).
> - $\exists v \in R: vu = 1$ (right-unit).
>
> `[Alu III.1.2]` `[Jud §16.1]`

> [!proposition] Properties of units — one-sided units, uniqueness of the inverse, the group of units
> In a ring $R$:
> - $u$ is a left- (resp., right-) unit iff left- (resp., right-) multiplication by $u$ is a [[knowledge/math/property/map/Surjection\|Surjection]] on $R$.
> - If $u$ is a left- (resp., right-) unit, then right- (resp., left-) multiplication by $u$ is an [[knowledge/math/property/map/Injection\|Injection]]; that is, $u$ is not a right- (resp., left-) zero-divisor.
> - The inverse of a two-sided unit is unique.
> - Two-sided units form a [[knowledge/math/algebra/structures/group/Group\|Group]] under multiplication.
>
> `[Alu III.1.2]` `[Jud Ex 16.7.35]` (the group of units $U(R)$)

### Characteristic

> [!definition] Parameters
> - $R$: a ring.
> - $\varphi: \mathbb Z \to R$: the unique [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]], $\varphi(m) = m \cdot 1_R$.

> [!definition] Characteristic
> As $\mathbb{Z}$ is the [[knowledge/math/algebra/structures/ring/Category Ring\|Initial Object]] of category $\mathsf{Ring}$, we have
> $$\exists n \in \mathbb{N}: \ker \varphi = n \mathbb{Z}.$$
> $n$ is called the **characteristic** of $R$.
>
> `[Alu III]`

> [!remark] The same number as in `[Jud]`
> `[Jud §16.2]` defines the characteristic as the least positive integer $n$ such that $nr = 0$ for all $r \in R$, and $0$ if there is no such integer. For a ring with $1$ this is the additive order of $1$ (`[Jud Lemma 16.2.7]`), which generates $\ker \varphi$: the two definitions agree.

## Property

> [!lemma] Annihilation — $0$ times anything is $0$
> In a ring $R$:
> $$\forall r \in R: 0 \cdot r = 0 = r \cdot 0$$
>
> `[Alu III.1]` `[Jud Prop 16.1.8]`

## Related

### Descendants
- [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]] — $ab = ba$; below it [[knowledge/math/algebra/structures/ring/special ring/Integral Domain\|Integral Domain]] and [[knowledge/math/algebra/structures/field/Field\|Field]].
- [[knowledge/math/algebra/structures/ring/special ring/Division Ring\|Division Ring]] — $1 \neq 0$ and every nonzero element is a two-sided unit.
- [[knowledge/math/algebra/structures/ring/special ring/Boolean Ring\|Boolean Ring]] — every element is idempotent.

### Instantiations
- [[knowledge/math/algebra/structures/ring/example/Zero Ring\|Zero Ring]] — the only ring with $0 = 1$.
- [[knowledge/math/algebra/structures/ring/example/Matrix Ring\|Matrix Ring]] — $M_n(R)$, not commutative for $n \geq 2$.
- [[knowledge/math/algebra/structures/ring/example/Monoid Ring\|Monoid Ring]] — $R[M]$, finite formal sums over a monoid.

### Constructions
- [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]] — a subset whose inclusion is a ring homomorphism.
- [[knowledge/math/algebra/structures/ring/subring/Ring Center\|Ring Center]] — the elements that commute with all of $R$.
- [[knowledge/math/algebra/structures/ring/special ring/Quotient Ring\|Quotient Ring]] — $R/I$ for a two-sided [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] $I$.
- [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]] — the maps; with them rings form [[knowledge/math/algebra/structures/ring/Category Ring\|$\mathsf{Ring}$]].

### Properties
- [[knowledge/math/algebra/structures/ring/Nilpotent Element\|Nilpotent Element]] — $a^n = 0$ for some positive integer $n$.

### Prerequisites
- [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]], [[knowledge/math/algebra/structures/Monoid\|Monoid]], [[knowledge/math/property/operation/Distributivity\|Distributivity]].
