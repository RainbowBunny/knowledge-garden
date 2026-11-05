---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/subgroup/centralizer/","dg-note-properties":{"aliases":["Centraliser"]}}
---

Reference:
- `[ConConj]` — K. Conrad, _Conjugation in a group_, expository notes, Definition 6.6, Theorem 6.7, equation (6.4): https://kconrad.math.uconn.edu/blurbs/grouptheory/conjclass.pdf

## Definition

> [!definition] Parameters
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]].
> - $g \in G$: an element.
> - $S \subseteq G$: a subset.

> [!definition] Centralizer
> The **centralizer** of $g$ is the set of elements of $G$ that commute with $g$:
> $$C_G(g) = \{x \in G \mid xg = gx\}.$$
> The centralizer of $S$ is the set of elements that commute with every element of $S$:
> $$C_G(S) = \{x \in G \mid xs = sx \text{ for all } s \in S\} = \bigcap_{s \in S} C_G(s).$$
>
> `[ConConj Def 6.6]` for $C_G(g)$, written $Z(g)$ there; the source notes that some books write $C(g)$.

## Property

> [!proposition] Stabilizer under conjugation — $C_G(g)$ is a subgroup
> **Scope**
> - $g \in G$.
>
> ---
> **Property**
> $C_G(g)$ is the [[knowledge/math/algebra/structures/action/Stabilizer\|Stabilizer]] of $g$ for the conjugation action of $G$ on itself ([[knowledge/math/algebra/structures/action/example/Group Action on Group\|Group Action on Group]]), hence a [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] of $G$.
>
> $C_G(S)$ is then a subgroup as an intersection of subgroups ([[knowledge/math/algebra/structures/group/subgroup/Subgroup#Property\|Subgroup#Property]]).

> [!theorem] Class size — the conjugacy class of $g$ has $[G : C_G(g)]$ elements
> **Scope**
> - $G$: a finite group.
> - $g \in G$.
>
> ---
> **Property**
> $$|\{xgx^{-1} \mid x \in G\}| = [G : C_G(g)].$$
>
> `[ConConj Thm 6.7]`, the [[knowledge/math/algebra/structures/action/Stabilizer#Property\|orbit–stabilizer theorem]] for conjugation. It gives the [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]].

> [!remark] The center
> $C_G(G) = Z(G)$, the [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]]; and $g \in Z(G)$ iff $C_G(g) = G$, iff the conjugacy class of $g$ is $\{g\}$.

## Example

> [!example] Centralizers
> - In an [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]], $C_G(g) = G$ for every $g$.
> - In the [[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]] $D_n$ with $n \geq 3$, the centralizer of the rotation $r$ is the rotation subgroup $\langle r \rangle$: a reflection $s$ satisfies $srs^{-1} = r^{-1} \neq r$.

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/subgroup/Normalizer\|Normalizer]] — the elements $x$ with $xHx^{-1} = H$, a weaker condition than commuting with each element of $H$
- [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]] — the centralizer of the whole group

### Prerequisites
- [[knowledge/math/algebra/structures/action/example/Group Action on Group\|Group Action on Group]], [[knowledge/math/algebra/structures/action/Stabilizer\|Stabilizer]]
