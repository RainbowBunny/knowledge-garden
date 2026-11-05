---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/example/zero-ring/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 1.2: First examples and special classes of rings; Exercise 1.1.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — §16.1 Rings; §16.3 Ring Homomorphisms and Ideals; Exercise 16.7.31 (read at the mirror https://judsonbooks.org/aata-files/aata-html/; item numbers as there).
- `[WP]` — Wikipedia, _Zero ring_: https://en.wikipedia.org/wiki/Zero_ring (read 2026-10-20).

## Definition

> [!definition] Parameters
> - $*$: the single element of the ring.

> [!definition] Zero-ring (Trivial Ring)
> Instantiates:: [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
>
> ---
> We define the zero-ring $(\{*\}, +, \cdot)$:
> - Elements of the ring is the [[knowledge/math/algebra/structures/group/example/Trivial Group\|trivial group]] $\{*\}$.
> - Operation of the ring:
> 	- $* + * = *$.
> 	- $* \cdot * = *$.
>
> Its single element is both the zero and the identity: $0 = 1 = *$.
>
> `[Alu III.1.2]` `[WP]`

## Property

> [!proposition] The only ring with $1 = 0$ — if $1 = 0$ in $R$, then $R$ is the zero ring
> If $1_R = 0_R$ in a [[knowledge/math/algebra/structures/ring/Ring\|Ring]] $R$, then $R = \{0\}$.
>
> `[Jud Ex 16.7.31]` `[WP]`

> [!proposition] No maps out — a homomorphism from the zero ring forces the target to be zero
> If there is a [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]] from a zero-ring to a [[knowledge/math/algebra/structures/ring/Ring\|Ring]] $R$, then $R$ is a zero-ring.
>
> `[Alu III]` `[WP]`

> [!remark] Both statements depend on the convention
> In `[Jud §16.1]` a ring with identity has $1 \neq 0$, so the zero ring is a ring but not a ring with identity. In `[Jud §16.3]` homomorphisms need not preserve $1$, so the zero map $\{0\} \to R$ is a homomorphism into every ring. The second proposition uses $\varphi(1) = 1$, as in [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]].

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/example/Trivial Group\|Trivial Group]] — the one-element group is both initial and final in [[knowledge/math/algebra/structures/group/Category Group\|Category Group]]; the zero ring has no ring homomorphism to a nonzero ring.

### Prerequisites
- [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
