---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/category-group/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter II: Groups, first encounter, Section 3.2: $\mathsf{Grp}$: Definition; Section 3.4: Product et al.
- `[Lei]` — T. Leinster, _Basic Category Theory_, arXiv:1612.09375: https://arxiv.org/abs/1612.09375

## Definition

> [!definition] Parameters
> - $G, H$: [[knowledge/math/algebra/structures/group/Group\|groups]].

> [!definition] Category $\mathsf{Grp}$
> Instantiates:: [[knowledge/math/algebra/category/Category\|Category]].
>
> ---
> $\mathsf{Grp}$ consists of
> - $\mathsf{Obj}(\mathsf{Grp})$ is the class of all [[knowledge/math/algebra/structures/group/Group\|Group]].
> - For $G, H$ groups, we define
> $$\mathsf{Hom}_\mathsf{Grp}(G, H)$$
> to be the set of [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] $G \rightarrow H$.
>
> `[Alu II.3.2]` `[Lei Ex 1.1.3(b)]`

## Property

### Universal Property

> [!proposition] Initial and Final Object — the trivial group is both
> [[knowledge/math/algebra/structures/group/example/Trivial Group\|Trivial Group]] are both [[knowledge/math/algebra/category/Universal Property\|Initial]] and [[knowledge/math/algebra/category/Universal Property\|Final]] in $\mathsf{Grp}$. `[Alu II.3]`

### Product

> [!proposition] Product — the direct product is the categorical product
> With operation defined component-wise, $G \times H$ is a [[knowledge/math/algebra/category/Categorical Product\|Product]] in $\mathsf{Grp}$. `[Alu II.3.4]`

## Related

### Prerequisites
- [[knowledge/math/algebra/category/Category\|Category]], [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] — the objects and morphisms

### Siblings
- [[knowledge/math/algebra/structures/group/Category Abelian\|Category Abelian]] — the full subcategory of $\mathsf{Grp}$ on the abelian groups `[Lei §1.2]`
- [[knowledge/math/algebra/structures/action/Category G-Set\|Category G-Set]] — the sets with an action of one fixed group
