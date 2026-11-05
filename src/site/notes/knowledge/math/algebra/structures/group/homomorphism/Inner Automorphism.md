---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/homomorphism/inner-automorphism/","dg-note-properties":{"aliases":["Inner Automorphism Group","Inn(G)"]}}
---

Reference:
- `[ConConj]` — K. Conrad, _Conjugation in a group_, expository notes, Theorem 3.5: https://kconrad.math.uconn.edu/blurbs/grouptheory/conjclass.pdf
- `[ConDih]` — K. Conrad, _Dihedral groups_, expository notes, Theorem 3.4: https://kconrad.math.uconn.edu/blurbs/grouptheory/dihedral.pdf

## Definition

> [!definition] Parameters
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]].
> - $g \in G$.

> [!definition] Inner Automorphism
> The **inner automorphism** of $G$ given by $g$ is conjugation by $g$:
> $$\gamma_g : G \to G, \qquad x \mapsto gxg^{-1}.$$
> It is an automorphism of $G$ ([[knowledge/math/algebra/structures/group/homomorphism/Group Isomorphism\|Group Isomorphism]]). The inner automorphisms form the set $\mathrm{Inn}(G) = \{\gamma_g \mid g \in G\}$.
>
> `[ConConj Thm 3.5]`

## Property

> [!proposition] $\mathrm{Inn}(G) \cong G / Z(G)$
> **Scope**
> - $\gamma : G \to \mathrm{Aut}(G)$, $g \mapsto \gamma_g$.
>
> ---
> **Property**
> - $\gamma$ is a [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]], with image $\mathrm{Inn}(G)$ and kernel the [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]] $Z(G)$.
> - $\mathrm{Inn}(G) \cong G / Z(G)$.
>
> $\gamma_g \gamma_h = \gamma_{gh}$, and $\gamma_g = \mathrm{id}$ iff $g$ commutes with every element. The center is defined as this kernel in [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]]; the [[knowledge/math/set theory/function/Canonical Decomposition\|first isomorphism theorem]] gives the isomorphism.

> [!proposition] Normal in $\mathrm{Aut}(G)$
> **Scope**
> - $\varphi \in \mathrm{Aut}(G)$, $g \in G$.
>
> ---
> **Property**
> $$\varphi \circ \gamma_g \circ \varphi^{-1} = \gamma_{\varphi(g)},$$
> so $\mathrm{Inn}(G) \trianglelefteq \mathrm{Aut}(G)$.
>
> Direct check: $\varphi(g \varphi^{-1}(x) g^{-1}) = \varphi(g)\, x\, \varphi(g)^{-1}$.

## Example

> [!example] Inner automorphism groups
> - $G$ abelian: $\mathrm{Inn}(G)$ is trivial.
> - The [[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]] $D_n$ with $n \geq 3$ odd has trivial center `[ConDih Thm 3.4]`, so $\mathrm{Inn}(D_n) \cong D_n$.

## Related

### Constructions
- [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]] — inside $G$, $H \rtimes K$ uses the inner automorphisms of $G$ restricted to $H$
- [[knowledge/math/algebra/structures/group/extension/Cyclic Extension\|Cyclic Extension]] — $\tau^n = \gamma_v$ is the condition on an extension type

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]], [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]], [[knowledge/math/algebra/structures/group/homomorphism/Group Isomorphism\|Group Isomorphism]]
