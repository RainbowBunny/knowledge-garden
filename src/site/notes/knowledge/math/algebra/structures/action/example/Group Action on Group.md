---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/action/example/group-action-on-group/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter II: Groups, first encounter, Section 9.2: Action on sets.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the LibreTexts copy, item numbers as there: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_%28Judson%29), §9.1 Isomorphisms; §14.1 Groups Acting on Sets.
- `[Con]` — K. Conrad, _Group actions_ (expository notes), Examples 2.10, 2.11: https://kconrad.math.uconn.edu/blurbs/grouptheory/gpaction.pdf

## Definition

> [!definition] Parameters
> - [[knowledge/math/algebra/structures/group/Group\|Group]]: Import $(G, \star, e_G)$.

> [!definition] Left-Multiplication
> Instantiates:: [[knowledge/math/algebra/structures/action/Group Action\|Group Action]].
>
> ---
> - Object: The [[knowledge/math/algebra/structures/group/Group\|Group]] $G$ itself.
> - The function $\rho: G \times G \rightarrow G$ is the operation in the group:
> $$(\forall g, a \in G): \rho(g, a) = g a$$
> `[Alu II.9.2]` `[Jud Ex 14.3]` `[Con Ex 2.10]`

> [!definition] Conjugation
> Instantiates:: [[knowledge/math/algebra/structures/action/Group Action\|Group Action]].
>
> ---
> - Object: The [[knowledge/math/algebra/structures/group/Group\|Group]] $G$ itself.
> - The function $\rho: G \times G \rightarrow G$ is the conjugation in the group:
> $$(\forall g, h \in G): \rho(g, h) = g h g^{-1}$$
> `[Alu II.9.2]` `[Jud Ex 14.4]` (there for a subgroup $H$; here $H = G$) `[Con Ex 2.11]`

## Property

Left-multiplication is faithful: $g \mapsto (a \mapsto ga)$ is the left regular representation, which proves [[knowledge/math/algebra/structures/action/Group Action#Property\|Cayley's theorem]] `[Jud Thm 9.12]`.

## Related

### Prerequisites
- [[knowledge/math/algebra/structures/action/Group Action\|Group Action]] — the structure both examples instantiate

### Constructions
- [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]] — the kernel of the conjugation action
