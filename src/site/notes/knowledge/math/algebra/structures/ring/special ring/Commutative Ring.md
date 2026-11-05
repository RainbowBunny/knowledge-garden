---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/special-ring/commutative-ring/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 1.2: First examples and special classes of rings.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — §16.1 Rings (read at the mirror https://judsonbooks.org/aata-files/aata-html/; item numbers as there).

## Definition

> [!definition] Parameters
> - [[knowledge/math/algebra/structures/ring/Ring\|Ring]]: Import $(R, +, *)$.

> [!definition] Commutative Ring
> Extends:: [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
>
> ---
> A [[knowledge/math/algebra/structures/ring/Ring\|Ring]] $(R, +, *)$ is a commutative ring if it also satisfies [[knowledge/math/property/operation/Commutativity\|Commutativity]] for $*$.
>
> `[Alu III.1.2]` `[Jud §16.1]`

## Related

### Descendants
- [[knowledge/math/algebra/structures/ring/special ring/Integral Domain\|Integral Domain]] — nonzero, with no zero divisors.
- [[knowledge/math/algebra/structures/field/Field\|Field]] — nonzero, every nonzero element is a unit.
- [[knowledge/math/algebra/structures/ring/ideal/Noetherian Ring\|Noetherian Ring]] — every ideal is finitely generated.

### Instantiations
- [[knowledge/math/algebra/structures/ring/example/Rings of Power Series\|Rings of Power Series]] — $R[\![x]\!]$ over a commutative ring $R$.

### Constructions
- [[knowledge/math/algebra/structures/ring/Commutative Ring Category\|Commutative Ring Category]] — commutative rings with a map from a set $A$; its initial object is the polynomial ring $\mathbb Z[x_1, \dots, x_n]$.

### Siblings
- [[knowledge/math/algebra/structures/ring/special ring/Boolean Ring\|Boolean Ring]] — always commutative, by a theorem rather than an axiom.
