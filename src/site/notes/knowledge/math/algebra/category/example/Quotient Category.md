---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/category/example/quotient-category/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter I: Preliminaries: Set theory and categories, Section 5.3: Quotients.
- `[Rie]` — E. Riehl, _Category Theory in Context_ (2016): https://math.jhu.edu/~eriehl/context.pdf — Exercise 1.1.iii (read at the mirror https://www.math.ucla.edu/~mopie/context.pdf).
- `[Ter]` — I. Terek, _Equivalence relations, quotients, and examples_ (lecture notes): https://web.williams.edu/Mathematics/it3/texts/quotients.pdf — Theorem 1.

## Definition

> [!definition] Parameters
> - $A$: a [[knowledge/math/set theory/Set\|Set]].
> - $\sim$: an [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] on $A$.

> [!definition] Quotient Category
> Instantiates:: [[knowledge/math/algebra/category/Category\|Category]].
>
> ---
> Let $\sim$ be an [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] on a set $A$.
> Quotient Category consists of
> - Object: $(\varphi, Z)$ where $Z$ is a set and [[knowledge/math/algebra/category/Morphism\|Morphism]] $\varphi: A \rightarrow Z$ such that:
> $$a_1 \sim a_2 \implies \varphi(a_1) = \varphi(a_2).$$
> - For $(\varphi_1, Z_1)$ and $(\varphi_2, Z_2)$, the morphisms are the functions $\sigma: Z_1 \to Z_2$ such that this diagram
> $$\begin{CD}
> Z_1 @>\sigma>> Z_2 \\
> @A\varphi_1AA @AA\varphi_2A \\
> A @= A
> \end{CD}$$
> commutes.
>
> `[Alu I.5.3]` `[Ter Thm 1]`

> [!remark]
> The objects are objects of the [[knowledge/math/algebra/category/example/Coslice Category\|Coslice Category]] $\mathsf{Set}^A$ (morphisms out of $A$, `[Rie Exer 1.1.iii]`) and the morphisms are exactly those of $\mathsf{Set}^A$: this is the full subcategory of $\mathsf{Set}^A$ on the functions constant on $\sim$-classes.

## Property

### Universal Property

> [!proposition] Quotient as initial object — $(\pi, A/{\sim})$ is initial
> Denoting by $\pi$ the [[knowledge/math/set theory/function/Canonical Projection\|Canonical Projection]], the pair $(\pi, A/_\sim)$ is an [[knowledge/math/algebra/category/Universal Property\|initial object]] of this category. `[Alu I.5.3]` `[Ter Thm 1]`

## Related

### Siblings
- [[knowledge/math/set theory/relation/Quotient Relation\|Quotient Relation]] — the quotient $A/{\sim}$ whose projection is initial here.

### Prerequisites
- [[knowledge/math/algebra/category/example/Coslice Category\|Coslice Category]] — the ambient category $\mathsf{Set}^A$.
- [[knowledge/math/set theory/function/Canonical Projection\|Canonical Projection]] — the map $\pi: A \to A/{\sim}$.
