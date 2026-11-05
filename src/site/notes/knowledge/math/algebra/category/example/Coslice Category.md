---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/category/example/coslice-category/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter I: Preliminaries: Set theory and categories, Exercise 3.7.
- `[Rie]` — E. Riehl, _Category Theory in Context_ (2016): https://math.jhu.edu/~eriehl/context.pdf — Exercise 1.1.iii (read at the mirror https://www.math.ucla.edu/~mopie/context.pdf).

## Definition

> [!definition] Parameters
> - $\mathsf C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A$: an object of $\mathsf C$.

> [!definition] Coslice Category
> Instantiates:: [[knowledge/math/algebra/category/Category\|Category]].
>
> ---
> Let $\mathsf{C}$ be a [[knowledge/math/algebra/category/Category\|Category]], and let $A \in \mathsf{Obj}(\mathsf{C})$, we define the coslice category $\mathsf{C}^A$ consists of:
> - $\mathsf{Obj}(\mathsf{C}^A)$: All [[knowledge/math/algebra/category/Morphism\|Morphism]] from $A$ to any object.
> - For $\varphi_1 \in \mathsf{Hom}_\mathsf{C}(A, Z_1)$ and $\varphi_2 \in \mathsf{Hom}_\mathsf{C}(A, Z_2)$, define $\mathsf{Hom}_{\mathsf{C}^A}(\varphi_1, \varphi_2)$ is the set of $\sigma \in \mathsf{Hom}_\mathsf{C}(Z_1, Z_2)$ such that this diagram
> $$\begin{CD}
> Z_1 @>\sigma>> Z_2 \\
> @A\varphi_1AA @AA\varphi_2A \\
> A @= A
> \end{CD}$$
> commutes, i.e. $\sigma \circ \varphi_1 = \varphi_2$.
>
> `[Alu Exer I.3.7]` `[Rie Exer 1.1.iii]`

> [!remark] Notation
> `[Rie Exer 1.1.iii]` writes $A/\mathsf C$ and calls it the slice category of $\mathsf C$ *under* $A$.

## Related

### Siblings
- [[knowledge/math/algebra/category/example/Slice Category\|Slice Category]] — the dual: objects are morphisms *into* $A$.
- [[knowledge/math/algebra/category/example/Quotient Category\|Quotient Category]] — a full subcategory of the coslice category $\mathsf{Set}^A$.
