---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/homomorphism/group-homomorphism/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter II: Groups, first encounter, Section 3.1: Group homomorphism; Section 3.3: Pause for reflection; Section 4.3: Isomorphisms; Section 6.2: Examples: Kernel and image; Section 6.5: Monomorphisms; Section 8.1: Canonical decomposition.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the LibreTexts copy, item numbers as there: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_%28Judson%29), §9.1 Isomorphisms; §11.1 Group Homomorphisms; §11.2 The Isomorphism Theorems.

## Definition

> [!definition] Parameters
> - $(G, \star_G)$, $(H, \star_H)$: [[knowledge/math/algebra/structures/group/Group\|groups]], with identities $e_G$, $e_H$.
> - $\varphi: G \to H$: a [[knowledge/math/set theory/Function\|Function]].

> [!definition] Group Homomorphism
> Extends:: [[knowledge/math/property/map/Homomorphism\|Homomorphism]].
>
> ---
> Let $(G, \star_G)$ and $(H, \star_H)$ be groups. A function $\varphi: G \rightarrow H$ is called a **(groups) homomorphism** if it satisfies $$\varphi(g_1 \star_G g_2) = \varphi(g_1) \star_H \varphi(g_2) \; \forall g_1, g_2 \in G.$$
> `[Alu II.3.1]` `[Jud §11.1]`

> [!definition] Group Homomorphism (Category Definition)
> The function $\varphi: G \rightarrow H$ defines a **group homomorphism** if this diagram commutes.
> $$\begin{CD} 
> G \times G @>\varphi \times \varphi>> H \times H\\ 
> @V\star_GVV @VV\star_HV\\ 
> G @>>\varphi> H 
> \end{CD}$$
> `[Alu II.3.1]`

### Kernel

Specializes [[knowledge/math/set theory/function/Kernel\|Kernel]].

$\ker \varphi = \varphi^{-1}(e_H)$; it is a [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]] of $G$ `[Jud Thm 11.5]`. The full note is [[knowledge/math/algebra/structures/group/subgroup/Kernel of Group Homomorphism\|Kernel of Group Homomorphism]].

### Group Isomorphism

Specializes [[knowledge/math/algebra/category/Morphism#Isomorphism\|Isomorphism]]; the note of its own is [[knowledge/math/algebra/structures/group/homomorphism/Group Isomorphism\|Group Isomorphism]].

> [!proposition] Isomorphism criterion — a group homomorphism is an isomorphism iff it is bijective
> Let $\varphi: G \rightarrow H$ be a group homomorphism. Then $\varphi$ is an isomorphism of groups if and only if it is a bijection. `[Alu II.4.3]`

> [!definition] Isomorphic
> Two groups $G, H$ are **isomorphic** if there is a bijective group homomorphism $G \rightarrow H$. `[Alu II.4.3]` `[Jud §9.1]`

> [!proposition] Isomorphisms preserve order and commutativity
> Let $\varphi: G \rightarrow H$ be an isomorphism
> - $(\forall g \in G): |\varphi(g)| = |g|$;
> - $G$ is commutative if and only if $H$ is commutative.
>
> `[Alu II.4.3]` `[Jud Thm 9.6]`

### Monomorphisms

Specializes [[knowledge/math/algebra/category/Morphism#Monomorphism\|Monomorphism]].

> [!proposition] Monomorphism criterion — monomorphism, trivial kernel and injectivity are equivalent
> The following are equivalent:
> - $\varphi$ is a monomorphism;
> - $\ker \varphi = \{e_G\}$;
> - $\varphi: G \rightarrow G'$ is injective (as a set-function).
>
> `[Alu II.6.5]`

## Property

> [!corollary] Surjective homomorphisms — $G' \cong G / \ker\varphi$ (first isomorphism theorem)
> Suppose $\varphi: G \rightarrow G'$ is a [[knowledge/math/property/map/Surjection\|Surjective]] group homomorphism. Then
> $$G' \cong \frac{G}{\ker{\varphi}}.$$
>
> ---
> Apply the [[knowledge/math/set theory/function/Canonical Decomposition\|Group Homomorphism Canonical Decomposition]].
>
> `[Alu II.8.1]` `[Jud Thm 11.10]`

### Inverse

> [!proposition] Identity and inverses are preserved
> Let $e_G$ be the identity element of $G$, let $e_H$ be the identity element of $H$, and let $g \in G$. Then
> - $\varphi(e_G) = e_H$;
> - $\varphi(g^{-1}) = \varphi(g)^{-1}$.
>
> `[Jud Prop 11.4]`

## Example

> [!example]
> Each of the following maps is a group homomorphism
> 1. The map $\phi : \mathbb Z \rightarrow \mathbb Z / N \mathbb Z$ that sends $a \in \mathbb Z$ to $a \mod N$ in $\mathbb Z / N \mathbb Z$.
> 2. The map $\phi : \mathbb R^* \rightarrow GL_2(\mathbb R)$ defined by $\phi(a) = \begin{pmatrix}a & 0 \\ 0 & a^{-1}\end{pmatrix}.$

## Related

### Descendants
- [[knowledge/math/algebra/structures/group/homomorphism/Group Isomorphism\|Group Isomorphism]] — a bijective group homomorphism

### Constructions
- [[knowledge/math/algebra/structures/group/subgroup/Kernel of Group Homomorphism\|Kernel of Group Homomorphism]] — the preimage of the identity
- [[knowledge/math/set theory/function/Canonical Decomposition\|Canonical Decomposition]] — every homomorphism factors through $G / \ker\varphi$
- [[knowledge/math/algebra/structures/group/Category Group\|Category Group]] — group homomorphisms are its morphisms

### Siblings
- [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]] — also preserves multiplication and $1$

### Prerequisites
- [[knowledge/math/property/map/Homomorphism\|Homomorphism]] — the origin, over any signature
- [[knowledge/math/algebra/structures/group/Group\|Group]]
