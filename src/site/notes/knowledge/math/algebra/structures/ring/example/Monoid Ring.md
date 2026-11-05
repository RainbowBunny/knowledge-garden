---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/example/monoid-ring/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 1.4: Monoid rings.
- `[WP]` — Wikipedia, _Monoid ring_: https://en.wikipedia.org/wiki/Monoid_ring (read 2026-10-20).

## Definition

> [!definition] Parameters
> - $(M, \cdot)$: a [[knowledge/math/algebra/structures/Monoid\|Monoid]] with identity $1_M$.
> - $R$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]] with identity $1_R$.
> - $A, B$: elements of $R[M]$, with coefficients $a_m, b_m \in R$.

> [!definition] Monoid Ring
> Instantiates:: [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
>
> ---
> For a monoid $(M, \cdot)$ and a ring $R$, we can obtain a new ring $(R[M], +, \cdot)$:
> - Elements of the ring are the formal sums $\sum_{m \in M} a_m \cdot m$ with $a_m \in R$ and $a_m = 0$ for all but finitely many $m \in M$.
> - Let $A = \sum_{m \in M} a_m \cdot m$ and $B = \sum_{m \in M} b_m \cdot m$:
> 	- $A + B = \sum_{m \in M} (a_m + b_m) \cdot m$.
> 	- $A \cdot B = \sum_{m \in M} \sum_{m_1 \cdot m_2 = m} (a_{m_1} b_{m_2}) \cdot m$.
> - The identity in $R[M]$ is $1_R \cdot 1_M$.
>
> `[Alu III.1.4]` `[WP]`

## Property

> [!proposition] Polynomials as a monoid ring — $R[(\mathbb N, +)]$ is the polynomial ring $R[x]$
> For the additive monoid $(\mathbb N, +)$, writing $x^k$ for $k \in \mathbb N$, the monoid ring $R[\mathbb N]$ is the [[knowledge/math/algebra/structures/polynomial/Polynomial Ring\|Polynomial Ring]] $R[x]$.
>
> `[WP]`

## Related

### Siblings
- [[knowledge/math/algebra/structures/polynomial/Polynomial Ring\|Polynomial Ring]] — the case $M = (\mathbb N, +)$.
- [[knowledge/math/algebra/structures/ring/example/Group Algebra\|Group Algebra]] — the case where $M$ is a group.
- [[knowledge/math/algebra/structures/ring/example/Rings of Power Series\|Rings of Power Series]] — sequences indexed by $\mathbb N$ as in $R[\mathbb N]$, without the finiteness condition.

### Prerequisites
- [[knowledge/math/algebra/structures/Monoid\|Monoid]], [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
