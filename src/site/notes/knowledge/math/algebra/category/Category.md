---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/category/category/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter I: Preliminaries: Set theory and categories, Section 3.1: Definition.
- `[Lei]` — T. Leinster, _Basic Category Theory_ (2014), arXiv:1612.09375 — Definition 1.1.1; Example 1.1.8(d), (e).
- `[Rie]` — E. Riehl, _Category Theory in Context_ (2016): https://math.jhu.edu/~eriehl/context.pdf — Definition 1.1.1; Example 1.1.3(i); Example 1.1.4(ii), (iii) (read at the mirror https://www.math.ucla.edu/~mopie/context.pdf).

## Definition

> [!definition] Parameters
> - $A, B, C, D$: objects of $\mathsf C$.
> - $f \in \mathsf{Hom}_\mathsf{C}(A, B)$: a morphism.
> - $g \in \mathsf{Hom}_\mathsf{C}(B, C)$: a morphism.
> - $h \in \mathsf{Hom}_\mathsf{C}(C, D)$: a morphism.

> [!definition] Category
> A **category** $\mathsf{C}$ consists of:
> - A collection of Object $\mathsf{Obj}(\mathsf{C})$.
> - A collection of [[knowledge/math/algebra/category/Morphism\|Morphism]] (arrow) $\mathsf{Hom}_{\mathsf{C}}(A, B)$ for each pair of objects $A, B$.
> - For each object $A$, an identity morphism $1_A \in \mathsf{Hom}_\mathsf{C}(A, A)$.
> - For each three objects $A, B, C$, an operation called [[knowledge/math/set theory/Function#Composition\|Composition]]
> $$\circ: \mathsf{Hom}_\mathsf{C}(A, B) \times \mathsf{Hom}_\mathsf{C}(B, C) \to \mathsf{Hom}_\mathsf{C}(A, C), \quad (f, g) \mapsto g \circ f,$$
>   which is [[knowledge/math/property/operation/Associativity\|Associative]] and has the identities as two-sided [[knowledge/math/property/operation/Identity Element\|identities]]:
>     - $h \circ (g \circ f) = (h \circ g) \circ f$;
>     - $f \circ 1_A = f$;
>     - $1_B \circ f = f$.
> - The sets $\mathsf{Hom}_{\mathsf{C}}(A, B)$ and $\mathsf{Hom}_{\mathsf{C}}(C, D)$ be *disjoint* unless $(A, B) = (C, D)$.
>
> `[Alu I.3.1]` `[Lei Def 1.1.1]` `[Rie Def 1.1.1]`

> [!remark]
> $f \in \mathsf{Hom}_{\mathsf{C}}(A, B)$ is the general form of $f: A \rightarrow B$.

> [!remark]
> In place of the disjointness clause, `[Rie Def 1.1.1]` gives each morphism a specified domain and codomain; the two say the same thing.

## Example

- [[knowledge/math/algebra/category/example/Category Set\|Category Set]] — sets and functions. `[Rie Ex 1.1.3(i)]`
- A [[knowledge/math/algebra/structures/Monoid\|Monoid]] is a category with one object — see [[knowledge/math/algebra/structures/Monoid\|Monoid]]. `[Rie Ex 1.1.4(ii)]` `[Lei Ex 1.1.8(d)]`
- A [[knowledge/math/set theory/relation/Preorder\|Preorder]] is a category with at most one morphism between two objects — see [[knowledge/math/algebra/category/example/Equivalence Category\|Equivalence Category]]. `[Rie Ex 1.1.4(iii)]` `[Lei Ex 1.1.8(e)]`

## Related

### Descendants
- [[knowledge/math/algebra/category/example/Groupoid\|Groupoid]] — every morphism is an [[knowledge/math/algebra/category/Morphism#Isomorphism\|isomorphism]].

### Instantiations
| | objects | morphisms |
| --- | --- | --- |
| [[knowledge/math/algebra/category/example/Category Set\|Category Set]] | sets | functions |
| [[knowledge/math/algebra/structures/group/Category Group\|Category Group]] | groups | group homomorphisms |
| [[knowledge/math/algebra/structures/group/Category Abelian\|Category Abelian]] | abelian groups | group homomorphisms |
| [[knowledge/math/algebra/structures/ring/Category Ring\|Category Ring]] | rings | ring homomorphisms |
| [[knowledge/math/algebra/structures/action/Category G-Set\|Category G-Set]] | sets with a $G$-action | functions commuting with the actions |
| [[knowledge/math/algebra/category/example/Category Power Set\|Category Power Set]] | subsets of a set $S$ | one arrow $A \to B$ iff $A \subseteq B$ |
| [[knowledge/math/algebra/category/example/Equivalence Category\|Equivalence Category]] | elements of a set $S$ | one arrow $a \to b$ iff $a \sim b$ |
| [[knowledge/math/algebra/category/example/Slice Category\|Slice Category]] | morphisms into a fixed $A$ | commuting triangles over $A$ |
| [[knowledge/math/algebra/category/example/Coslice Category\|Coslice Category]] | morphisms out of a fixed $A$ | commuting triangles under $A$ |
| [[knowledge/math/algebra/category/example/Quotient Category\|Quotient Category]] | functions out of $A$ constant on $\sim$-classes | commuting triangles under $A$ |
| [[knowledge/math/algebra/category/Opposite Category\|Opposite Category]] | the objects of $\mathsf C$ | the morphisms of $\mathsf C$, reversed |

### Prerequisites
- [[knowledge/math/algebra/category/Morphism\|Morphism]] — the arrows, and isomorphism, mono, epi, endo, auto.
