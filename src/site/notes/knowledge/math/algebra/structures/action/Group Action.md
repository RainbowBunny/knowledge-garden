---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/action/group-action/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter II: Groups, first encounter, Section 9.1: Actions; Section 9.2: Actions on sets; Section 9.3: Transitive actions and the category G-Set.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the LibreTexts copy, item numbers as there: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_%28Judson%29), §9.1 Isomorphisms; §14.1 Groups Acting on Sets; §14.2 The Class Equation.
- `[Con]` — K. Conrad, _Group actions_ (expository notes): https://kconrad.math.uconn.edu/blurbs/grouptheory/gpaction.pdf
- `[Lei]` — T. Leinster, _Basic Category Theory_, arXiv:1612.09375, Example 1.2.8: https://arxiv.org/abs/1612.09375

## Definition

> [!definition] Parameters
> - [[knowledge/math/algebra/structures/group/Group\|Group]]: Import $(G, \star, e_G)$.
> - $\mathsf C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A$: an object of $\mathsf C$.
> - $\sigma: G \to \mathsf{Aut}_\mathsf{C}(A)$: the action.

> [!definition] Group Action
> An **action** of a [[knowledge/math/algebra/structures/group/Group\|Group]] $G$ on an object $A$ of a [[knowledge/math/algebra/category/Category\|Category]] $\mathsf{C}$ is a [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|homomorphism]]
> $$\sigma: G \rightarrow \mathsf{Aut}_\mathsf{C}(A).$$
> `[Alu II.9.1]`

### Action on a Set

> [!definition] Parameters
> - [[knowledge/math/algebra/structures/group/Group\|Group]]: Import $(G, \star, e_G)$.
> - $A$: a [[knowledge/math/set theory/Set\|Set]].
> - $\rho: G \times A \to A$: a [[knowledge/math/set theory/Function\|Function]], written $ga = \rho(g, a)$.

> [!definition] Action on Set
> An **action** of a [[knowledge/math/algebra/structures/group/Group\|Group]] $G$ on a [[knowledge/math/set theory/Set\|Set]] $A$ is a [[knowledge/math/set theory/Function\|Function]]
> $$\rho: G \times A \rightarrow A$$
> such that:
> - $\forall a \in A: \rho(e_G, a) = a$.
> - $(\forall g, h \in G), (\forall a \in A): \rho(gh, a) = \rho(g, \rho(h, a))$.
>
> Usually, we can just remove $\rho$ and have a simpler [[knowledge/math/property/operation/Associativity\|Associativity]] operation:
> $$(\forall g, h \in G), (\forall a \in A): (gh) a = g (ha).$$
> `[Alu II.9.2]` `[Jud §14.1]`

### Faithful

> [!definition] Faithful
> An action of a [[knowledge/math/algebra/structures/group/Group\|Group]] $G$ on an object $A$ of a [[knowledge/math/algebra/category/Category\|Category]] $\mathsf{C}$ is **faithful** (or **effective**) if the corresponding $\sigma: G \rightarrow \mathsf{Aut}_\mathsf{C}(A)$ is an [[knowledge/math/property/map/Injection\|Injection]]. `[Alu II.9.1]` `[Con Def 2.17]`

### Fixed Point

> [!definition] Parameters
> - $G$, $A$: a group acting on a set, as in *Action on a Set*.

> [!definition] Fixed Point
> $Z$ is the set of **fixed points** of the action:
> $$Z = \{a \in A \mid (\forall g \in G): ga = a\}$$
> `[Jud §14.2]`

## Property

> [!theorem] Cayley's theorem — every group is a subgroup of a symmetric group
> Every [[knowledge/math/algebra/structures/group/Group\|Group]] acts faithfully on some set. That is, every group may be realized as a [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] of a [[knowledge/math/algebra/structures/group/special group/Symmetric Group\|Symmetric Group]].
>
> ---
> [[knowledge/math/algebra/structures/action/example/Group Action on Group\|Left Multiplication]].
>
> `[Alu II.9.2]` `[Jud Thm 9.12]`

> [!proposition] Orbit decomposition — $|A|$ is the number of fixed points plus the sizes of the nontrivial orbits
> Let $A$ be finite, and let $B \subseteq A$ contain exactly one element of each nontrivial [[knowledge/math/algebra/structures/action/Orbit\|Orbit]] of the action; $G_a$ is the [[knowledge/math/algebra/structures/action/Stabilizer\|Stabilizer]] of $a$. Then,
> $$|A| = |Z| + \sum_{a \in B} |G : G_a|.$$
> `[Jud §14.2, Thm 14.11]` `[Con Thm 3.16(c)]`

> [!corollary] Fixed points of a $p$-group — $|Z| \equiv |A| \bmod p$
> With $G$ is a [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]] acting on a finite set $A$:
> $$|Z| \equiv |A| \mod p$$
> `[Con Thm 4.1]`

## Related

### Instantiations
- [[knowledge/math/algebra/structures/action/example/Group Action on Group\|Group Action on Group]] — $G$ acting on itself by left multiplication and by conjugation

### Constructions
- [[knowledge/math/algebra/structures/action/Orbit\|Orbit]] — the points reachable from one point
- [[knowledge/math/algebra/structures/action/Stabilizer\|Stabilizer]] — the subgroup fixing one point
- [[knowledge/math/algebra/structures/action/Burnside's Counting Theorem\|Burnside's Counting Theorem]] — the number of orbits is the average number of fixed points
- [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]] — the orbit decomposition of the conjugation action
- [[knowledge/math/algebra/structures/action/Category G-Set\|Category G-Set]] — the actions of $G$ on sets and the equivariant maps between them

### Siblings
- [[knowledge/math/algebra/structures/action/Group Representation\|Group Representation]] — an action on a vector space by linear maps `[Lei Ex 1.2.8]`

### Prerequisites
- [[knowledge/math/algebra/structures/group/Group\|Group]], [[knowledge/math/algebra/structures/group/special group/Symmetric Group\|Symmetric Group]], [[knowledge/math/algebra/category/Morphism#Automorphism\|Automorphism]]
