---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/category/categorical-coproduct/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter I: Preliminaries: Set theory and categories, Section 5.1: Initial and final objects; Section 5.5: Coproducts.
- `[nLab]` — nLab, _coproduct_: https://ncatlab.org/nlab/show/coproduct

## Definition

> [!definition] Parameters
> - $\mathsf C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A, B$: objects of $\mathsf C$.

> [!definition] Categorical Coproduct
> Requires:: [[knowledge/math/algebra/category/Universal Property\|Universal Property]].
>
> ---
> Let $A, B$ be objects of a [[knowledge/math/algebra/category/Category\|Category]] $\mathsf{C}$. A **coproduct** $A \amalg B$ of $A$ and $B$ will be an object $C$, endowed with two morphisms
> - $\iota_A: A \to C$,
> - $\iota_B: B \to C$,
>
> satisfying the following universal property: for all objects $Z$ and morphisms
> $$\begin{CD}
> A @>f_A>> Z \\
> @.   @|\\
> B @>>f_B> Z
> \end{CD}$$
> there exists a unique morphism $\sigma: A \amalg B \rightarrow Z$ such that the diagram
> $$\begin{CD}
> Z @= Z @= Z\\
> @A{f_A}AA @AA{\sigma}A @AA{f_B}A\\
> A @>>{\iota_A}> A \amalg B @<<{\iota_B}< B
> \end{CD}$$
> commutes. `[Alu I.5.5]` `[nLab]`

> [!remark]
> $\iota_A, \iota_B$ are called coprojections, or sometimes injections or inclusions; in a general category they need not be [[knowledge/math/algebra/category/Morphism#Monomorphism\|monomorphisms]]. `[nLab]`

## Example

- [[knowledge/math/algebra/category/example/Category Set\|Category Set]] — in $\mathsf{Set}$ the coproduct is the disjoint union. `[nLab]`

## Related

### Siblings
- [[knowledge/math/algebra/category/Categorical Product\|Categorical Product]] — the dual notion: the same universal property with every arrow reversed.
- [[knowledge/math/set theory/function/Natural Injection\|Natural Injection]] — a function; $\iota_A, \iota_B$ are morphisms of $\mathsf C$ and need not be injective.

### Prerequisites
- [[knowledge/math/algebra/category/Universal Property\|Universal Property]] — the form the definition takes.
