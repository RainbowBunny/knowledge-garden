---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/homomorphism/group-isomorphism/","dg-note-properties":{}}
---

Reference:
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the LibreTexts copy, item numbers as there: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_%28Judson%29), §9.1 Definition and Examples.

## Definition

> [!definition] Parameters
> - $(G, \cdot)$, $(H, \circ)$: [[knowledge/math/algebra/structures/group/Group\|groups]].
> - $\varphi: G \to H$: a [[knowledge/math/set theory/Function\|Function]].

> [!definition] Group Isomorphism
> Extends:: [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]].
>
> ---
> A **group isomorphism** is a [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] $\varphi: G \to H$ that is a [[knowledge/math/property/map/Bijection\|Bijection]] (one-to-one and onto):
> $$\forall a, b \in G: \quad \varphi(a \cdot b) = \varphi(a) \circ \varphi(b).$$
> $G$ and $H$ are **isomorphic**, written $G \cong H$, if such a $\varphi$ exists. `[Jud §9.1]`

## Property

> [!theorem] Isomorphisms transport structure — inverse, size, commutativity, cyclicity and subgroup orders carry over
> Let $\varphi: G \to H$ be an isomorphism. Then
> - $\varphi^{-1}: H \to G$ is an isomorphism;
> - $|G| = |H|$;
> - if $G$ is abelian, then $H$ is abelian;
> - if $G$ is cyclic, then $H$ is cyclic;
> - if $G$ has a subgroup of order $n$, then $H$ has a subgroup of order $n$.
>
> `[Jud Thm 9.6]`

## Related

### Prerequisites
- [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] — the parent; its section *Group Isomorphism* shows that the bijective homomorphisms are exactly the isomorphisms of [[knowledge/math/algebra/structures/group/Category Group\|Grp]]
- [[knowledge/math/algebra/category/Morphism#Isomorphism\|Isomorphism]] — the origin, in any category
