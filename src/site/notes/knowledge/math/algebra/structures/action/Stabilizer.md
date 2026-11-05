---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/action/stabilizer/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter IV: Groups, second encounter, Section 1.1: Actions of groups on sets, reminder.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the LibreTexts copy, item numbers as there: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_%28Judson%29), §14.1 Groups Acting on Sets.
- `[Con]` — K. Conrad, _Group actions_ (expository notes): https://kconrad.math.uconn.edu/blurbs/grouptheory/gpaction.pdf

## Definition

> [!definition] Parameters
> - [[knowledge/math/algebra/structures/action/Group Action\|Group Action]]: Import $(G, A, \rho)$, writing $ga = \rho(g, a)$.
> - $a \in A$: an element.

> [!definition] Stabilizer
> Requires:: [[knowledge/math/algebra/structures/action/Group Action\|Group Action]].
>
> ---
> The **stabilizer** [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] of $a$ consists of the elements of $G$ which fix $a$:
> $$\mathsf{Stab}_G(a) = \{g \in G \mid ga = a\}$$
> Also written $G_a$ (the *isotropy subgroup*). `[Alu IV.1.1]` `[Jud §14.1, Prop 14.10]`

## Property

> [!proposition] Transitive actions are coset actions — a transitive action is isomorphic to $G$ acting on $G / \mathsf{Stab}_G(a)$
> Every transitive (single-orbit) left-action of $G$ on a nonempty [[knowledge/math/set theory/Set\|Set]] $A$ is [[knowledge/math/algebra/category/Morphism#Isomorphism\|Isomorphic]] (in [[knowledge/math/algebra/structures/action/Category G-Set\|G-Set]]) to the left-multiplication of $G$ on $G/H$, for $H$ = the stabilizer of any $a \in A$.
>
> ---
> - $H = \mathsf{Stab}_G(a)$
> - $\varphi: G/H \rightarrow A,\quad gH \mapsto ga$
>
> `[Alu IV.1.1]` `[Con Thm 3.36]`

> [!corollary] Orbit–stabilizer theorem — $|O| \cdot |\mathsf{Stab}_G(a)| = |G|$, so $|O|$ divides $|G|$
> Requires:: [[knowledge/math/algebra/structures/group/special group/Coset\|Coset]].
>
> ---
> If $O$ is an orbit of the action of a finite [[knowledge/math/algebra/structures/group/Group\|Group]] $G$ on a [[knowledge/math/set theory/Set\|Set]] $A$, then $O$ is a finite set and
> $$|O| \mid |G|.$$
>
> ---
> $|O| \cdot |\mathsf{Stab}_G(a)| = |G|$ for any $a \in O$.
>
> `[Alu IV.1.1]` `[Jud Thm 14.11]` `[Con Thm 3.16(c)]`

> [!proposition] Stabilizers along an orbit are conjugate — $\mathsf{Stab}_G(ga) = g \, \mathsf{Stab}_G(a) \, g^{-1}$
> Suppose a [[knowledge/math/algebra/structures/group/Group\|Group]] $G$ acts on a [[knowledge/math/set theory/Set\|Set]] $A$; let $a \in A$ and $g \in G$, and put $b = ga$. Then
> $$\mathsf{Stab}_G(b) = g \mathsf{Stab}_G(a) g^{-1}$$
> `[Alu IV.1.1]` `[Con Thm 3.16(b)]`

## Related

### Prerequisites
- [[knowledge/math/algebra/structures/action/Group Action\|Group Action]] — the action whose stabilizers these are
- [[knowledge/math/algebra/structures/group/special group/Coset\|Coset]] — $G / \mathsf{Stab}_G(a)$ is a set of left cosets, not a quotient group in general

### Siblings
- [[knowledge/math/algebra/structures/action/Orbit\|Orbit]] — the points reached from $a$; in bijection with $G / \mathsf{Stab}_G(a)$
