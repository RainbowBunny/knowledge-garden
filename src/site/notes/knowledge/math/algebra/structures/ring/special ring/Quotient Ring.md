---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/special-ring/quotient-ring/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 3.2: Quotients.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — §16.3 Ring Homomorphisms and Ideals (read at the mirror https://judsonbooks.org/aata-files/aata-html/; item numbers as there).

## Definition

> [!definition] Parameters
> - $(R, +, \cdot)$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
> - $I$: a two-sided [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] of $R$.
> - $r$: an element of $R$.
> - $s$: an element of $R$.

> [!definition] Quotient Ring
> Extends:: [[knowledge/math/set theory/relation/Quotient Relation\|Quotient Relation]].
>
> ---
> Let $I$ be a two-sided [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] of the [[knowledge/math/algebra/structures/ring/Ring\|Ring]] $(R, +, \cdot)$. The **quotient ring** of $R$ **modulo** $I$, denoted $R / I$, is defined as the set of [[knowledge/math/algebra/structures/group/special group/Coset\|Coset]] $r + I$ of $I$, with the operations
> - $(r + I) + (s + I) = (r + s) + I$
> - $(r + I)(s + I) = rs + I$
>
> Its zero is $0 + I$ and its identity is $1 + I$.
>
> `[Alu III.3.2]` `[Jud Thm 16.3.10]`

## Property

> [!proposition] Canonical projection — $r \mapsto r + I$ is a surjective ring homomorphism with kernel $I$
> The map $\pi: R \to R/I$ given by $\pi(r) = r + I$ is a surjective [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]], and $\ker \pi = I$.
>
> `[Jud Thm 16.3.11]`

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/special group/Quotient Group\|Quotient Group]] — the same construction for a [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]]; for rings one divides by an ideal, which (if proper) is not a subring.
- [[knowledge/math/algebra/structures/polynomial/Quotient of Polynomial Ring\|Quotient of Polynomial Ring]] — the quotient of a polynomial ring by an ideal.

### Prerequisites
- [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]], [[knowledge/math/algebra/structures/group/special group/Coset\|Coset]].
- [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]] — the universal property of $R/I$ and the isomorphism theorems.
