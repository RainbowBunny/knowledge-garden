---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/category/example/groupoid/","dg-note-properties":{}}
---

Reference:
- `[Rie]` — E. Riehl, _Category Theory in Context_ (2016): https://math.jhu.edu/~eriehl/context.pdf — Definition 1.1.11; Lemma 1.1.13 (read at the mirror https://www.math.ucla.edu/~mopie/context.pdf).
- `[Lei]` — T. Leinster, _Basic Category Theory_ (2014), arXiv:1612.09375 — Example 1.1.8(c).

## Definition

> [!definition] Groupoid
> Extends:: [[knowledge/math/algebra/category/Category\|Category]].
>
> ---
> A [[knowledge/math/algebra/category/Category\|Category]] in which every morphism is an [[knowledge/math/algebra/category/Morphism#Isomorphism\|isomorphism]] is called a **groupoid**. `[Rie Def 1.1.11]`

## Property

> [!proposition] Maximal groupoid — every category contains one, on all of its objects
> Any category $\mathsf C$ contains a maximal groupoid: the subcategory containing all of the objects of $\mathsf C$ and only those morphisms that are isomorphisms. `[Rie Lemma 1.1.13]`

## Example

> [!example] A group is a one-object groupoid
> A [[knowledge/math/algebra/structures/group/Group\|Group]] is essentially a category with one object in which every morphism is an isomorphism: the morphisms are the elements of the group and composition is the group operation. `[Lei Ex 1.1.8(c)]`

## Related

### Siblings
- [[knowledge/math/algebra/structures/Magma\|Magma]] — a homonym: Burris–Sankappanavar call a magma a *groupoid*.
- [[knowledge/math/algebra/category/example/Equivalence Category\|Equivalence Category]] — a groupoid exactly when its relation is also symmetric.
