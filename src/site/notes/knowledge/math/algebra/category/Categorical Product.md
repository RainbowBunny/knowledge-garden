---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/category/categorical-product/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter I: Preliminaries: Set theory and categories, Section 5.1: Initial and final objects; Section 5.4: Products.
- `[nLab]` — nLab, _cartesian product_ (the binary product in a category): https://ncatlab.org/nlab/show/product

## Definition

> [!definition] Parameters
> - $\mathsf C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A, B$: objects of $\mathsf C$.

> [!definition] Categorical Product
> Requires:: [[knowledge/math/algebra/category/Universal Property\|Universal Property]].
>
> ---
> Let $A, B$ be objects of a category $\mathsf{C}$. A product $A \times B$ of $A$ and $B$ will be an object $C$, endowed with two morphisms, the projections
> - $\pi_A: C \to A$,
> - $\pi_B: C \to B$,
>
> satisfying the following universal property: for every object $Z$ and morphisms
> $$\begin{CD}
> A @<f_A<< Z \\
> @.   @|\\
> B @<<f_B< Z
> \end{CD}$$
> there exists a unique morphism $\sigma \in \mathsf{Hom}_{\mathsf{C}}(Z, A \times B)$ such that the diagram
> $$\begin{CD}
> Z @= Z @= Z\\
> @Vf_AVV @VV{\sigma}V @VVf_BV\\
> A @<{\pi_A}<< A\times B @>{\pi_B}>> B
> \end{CD}$$
> commutes. `[Alu I.5.4]` `[nLab]`

## Example

- [[knowledge/math/algebra/category/example/Category Set\|Category Set]] — in $\mathsf{Set}$ the product is the cartesian product of sets. `[nLab]`
- [[knowledge/math/algebra/structures/group/Category Group\|Category Group]] — in $\mathsf{Grp}$, $G \times H$ with the componentwise operation (its section Product).

## Related

### Siblings
- [[knowledge/math/algebra/category/Categorical Coproduct\|Categorical Coproduct]] — the dual notion: the same universal property with every arrow reversed.
- [[knowledge/math/set theory/function/Natural Projection\|Natural Projection]] — a function; $\pi_A, \pi_B$ are morphisms of $\mathsf C$ and need not be surjective.

### Prerequisites
- [[knowledge/math/algebra/category/Universal Property\|Universal Property]] — the form the definition takes.
