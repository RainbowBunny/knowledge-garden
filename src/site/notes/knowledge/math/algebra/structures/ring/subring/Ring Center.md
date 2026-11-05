---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/subring/ring-center/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Exercise 2.9.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — Exercise 16.7.32 (read at the mirror https://judsonbooks.org/aata-files/aata-html/; item numbers as there).
- `[WP]` — Wikipedia, _Division ring_: https://en.wikipedia.org/wiki/Division_ring (read 2026-10-20).

## Definition

> [!definition] Parameters
> - $R$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].

> [!definition] Ring Center
> Extends:: [[knowledge/math/algebra/structures/Center\|Center]].
> Requires:: [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
>
> ---
> The **center** of a [[knowledge/math/algebra/structures/ring/Ring\|Ring]] $R$, denoted $Z(R)$, consists of the elements $a$ such that $\forall r \in R: a r = r a$.
>
> `[Alu III Ex 2.9]` `[Jud Ex 16.7.32]`

## Property

> [!proposition] Center is a subring — $Z(R)$ is a commutative subring of $R$
> The center is a commutative [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]] of $R$.
>
> `[Alu III Ex 2.9]` `[Jud Ex 16.7.32]`

> [!proposition] Center of a division ring — it is a field
> The center of a [[knowledge/math/algebra/structures/ring/special ring/Division Ring\|Division Ring]] is a [[knowledge/math/algebra/structures/field/Field\|Field]].
>
> `[Alu III Ex 2.9]` `[WP]`

## Related

### Constructions
- [[knowledge/math/algebra/structures/ring/module/R-algebra\|R-algebra]] — a ring homomorphism $R \to S$ whose image lies in $Z(S)$.

### Siblings
- [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]] — the same construction in a [[knowledge/math/algebra/structures/group/Group\|Group]]; there the center is an abelian [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]].

### Prerequisites
- [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]], [[knowledge/math/algebra/structures/ring/special ring/Division Ring\|Division Ring]].
