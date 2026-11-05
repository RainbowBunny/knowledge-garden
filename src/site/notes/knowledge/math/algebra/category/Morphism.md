---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/category/morphism/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter I: Preliminaries: Set theory and categories, Section 4.1: Isomorphisms; Section 4.2: Monomorphisms and epimorphisms.
- `[Lei]` — T. Leinster, _Basic Category Theory_ (2014), arXiv:1612.09375 — Definition 1.1.4.
- `[Rie]` — E. Riehl, _Category Theory in Context_ (2016): https://math.jhu.edu/~eriehl/context.pdf — Definition 1.1.1; Definition 1.1.9 and the sentence after it; Exercise 1.1.i; Definition 1.2.7; Example 1.2.8 (read at the mirror https://www.math.ucla.edu/~mopie/context.pdf).

## Definition

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A, B$: objects of $\mathcal C$.

> [!definition] Morphism
> Requires:: [[knowledge/math/algebra/category/Category\|Category]].
>
> ---
> A morphism is a map between objects in an abstract [[knowledge/math/algebra/category/Category\|Category]]; the morphisms from $A$ to $B$ form $\mathsf{Hom}_{\mathcal C}(A, B)$. `[Rie Def 1.1.1]`

> [!definition] Parameters
> - $A$: an object of $\mathcal C$.

> [!definition] Identity Morphism
> We define the identity morphism $1_A \in \mathsf{Hom}_{\mathcal{C}}(A, A)$ that transform an object to itself. `[Rie Def 1.1.1]`

### Isomorphism

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A, B$: objects of $\mathcal C$.
> - $f \in \mathsf{Hom}_{\mathcal C}(A, B)$: a morphism.

> [!definition] Isomorphism
> Let $\mathcal C$ be a category. A morphism $f \in \mathsf{Hom}_{\mathcal{C}}(A, B)$ is an **isomorphism** if it has a (two-sided) inverse under composition: that is, if $\exists g \in \mathsf{Hom}_{\mathcal{C}}(B, A)$ such that
> - $gf = 1_A$,
> - $fg = 1_B$.
>
> `[Alu I.4.1]` `[Lei Def 1.1.4]` `[Rie Def 1.1.9]`

### Monomorphism

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A, B$: objects of $\mathcal C$.
> - $f \in \mathsf{Hom}_{\mathcal C}(A, B)$: a morphism.

> [!definition] Monomorphism
> Let $\mathcal C$ be a category. A morphism $f \in \mathsf{Hom}_{\mathcal{C}}(A, B)$ is a **monomorphism** if the following holds:
> - For all object $Z$ of $\mathcal C$ and all morphisms $\alpha', \alpha'' \in \mathsf{Hom}_{\mathcal{C}}(Z, A)$,
> $$f \circ \alpha' = f \circ \alpha'' \Longrightarrow \alpha' = \alpha''.$$
>
> `[Alu I.4.2]` `[Rie Def 1.2.7]`

### Epimorphism

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A, B$: objects of $\mathcal C$.
> - $f \in \mathsf{Hom}_{\mathcal C}(A, B)$: a morphism.

> [!definition] Epimorphism
> Let $\mathcal C$ be a category. A morphism $f \in \mathsf{Hom}_{\mathcal{C}}(A, B)$ is an **epimorphism** if the following holds:
> - For all object $Z$ of $\mathcal C$ and all morphisms $\beta', \beta'' \in \mathsf{Hom}_{\mathcal{C}}(B, Z)$:
> $$\beta' \circ f = \beta'' \circ f \Longrightarrow \beta' = \beta''.$$
>
> `[Alu I.4.2]` `[Rie Def 1.2.7]`

### Endomorphism

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A$: an object of $\mathcal C$.

> [!definition] Endomorphism
> A morphism of an object $A$ of a category $\mathcal C$ to itself is called an **endomorphism**; $\mathsf{Hom}_{\mathcal{C}}(A, A)$ is denoted $\mathsf{End}_{\mathcal{C}}(A)$. `[Alu I.4.1]` `[Rie Def 1.1.9]`

### Automorphism

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $A$: an object of $\mathcal C$.

> [!definition] Automorphism
> An **automorphism** of an object $A$ of a category $\mathcal C$ is an isomorphism from $A$ to itself. The set of automorphisms of $A$ is denoted $\mathsf{Aut}_{\mathcal{C}}(A)$; it is a subset of $\mathsf{End}_{\mathcal{C}}(A)$. `[Alu I.4.1]` `[Rie Def 1.1.9]`

## Property

### Isomorphisms

> [!proposition] Uniqueness of the inverse — an isomorphism has exactly one inverse
> The inverse of an isomorphism is unique. `[Alu I.4.1]` `[Rie Exer 1.1.i]`

> [!proposition] Isomorphisms are closed under identity, inverse and composition
> We denote inverse by $f^{-1}$.
> - Each identity $1_A$ is an isomorphism and is its own inverse.
> - If $f$ is an isomorphism, then $f^{-1}$ is an isomorphism and further $(f^{-1})^{-1} = f$.
> - If $f \in \mathsf{Hom}_{\mathcal C}(A, B)$ and $g \in \mathsf{Hom}_{\mathcal C}(B, C)$ are isomorphisms, then the composition $gf$ is an isomorphism and $(gf)^{-1} = f^{-1} g^{-1}$.
>
> `[Alu I.4.1]`

> [!corollary] Isomorphism is an equivalence relation — on the objects of $\mathcal C$
> Isomorphism is an equivalence relation. If two objects $A, B$ are isomorphic, one writes $A \cong B$. `[Alu I.4.1]`

### In the category of sets

> [!proposition] Monomorphisms in Set — they are the injective functions
> In [[knowledge/math/algebra/category/example/Category Set\|$\mathsf{Set}$]], a [[knowledge/math/set theory/Function\|Function]] $f: A \rightarrow B$ is an [[knowledge/math/property/map/Injection\|Injection]] if and only if it is a monomorphism. `[Alu I.4.2]` `[Rie Ex 1.2.8]`

> [!proposition] Epimorphisms in Set — they are the surjective functions
> In [[knowledge/math/algebra/category/example/Category Set\|$\mathsf{Set}$]], a [[knowledge/math/set theory/Function\|Function]] $f: A \rightarrow B$ is a [[knowledge/math/property/map/Surjection\|Surjection]] if and only if it is an epimorphism. `[Alu I.4.2]` `[Rie Ex 1.2.8]`

### Automorphism group

> [!proposition] Automorphism group — $\mathsf{Aut}_{\mathcal C}(A)$ is a group under composition
> - The composition of two elements $f, g \in \mathsf{Aut}_{\mathcal{C}}(A)$ is an element $gf \in \mathsf{Aut}_{\mathcal{C}}(A)$.
> - Composition is associative.
> - $\mathsf{Aut}_{\mathcal{C}}(A)$ contains the element $1_A$, which is an identity for composition.
> - Every element $f \in \mathsf{Aut}_{\mathcal{C}}(A)$ has an inverse $f^{-1} \in \mathsf{Aut}_{\mathcal{C}}(A)$.
>
> `[Alu I.4.1]`

## Related

### Descendants
| where | what the structure adds |
| --- | --- |
| [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]], sections Group Isomorphism and Monomorphisms | an isomorphism of groups is exactly a bijective homomorphism; a monomorphism is exactly one with $\ker \varphi = \{e_G\}$, i.e. an injective one |
| [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]], sections Ring Isomorphism and Ring Monomorphism | a monomorphism is exactly one with $\ker \varphi = \{0\}$, i.e. an injective one |
| [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]], section Invertibility | an invertible linear map is an isomorphism; invertible iff injective and surjective |

### Siblings
- [[knowledge/math/property/map/Homomorphism\|Homomorphism]] — a structure-preserving function; the morphisms of [[knowledge/math/algebra/structures/group/Category Group\|Category Group]] and [[knowledge/math/algebra/structures/ring/Category Ring\|Category Ring]] are homomorphisms.

### Prerequisites
- [[knowledge/math/algebra/category/Category\|Category]] — where morphisms live.
