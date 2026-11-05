---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/ring-homomorphism/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 2.1: Ring homomorphisms; Section 2.3: Monomorphisms and epimorphisms; Section 3.1: Ideals; Section 3.2: Quotients; Section 3.3: Canonical decomposition and consequences.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — §16.3 Ring Homomorphisms and Ideals (read at the mirror https://judsonbooks.org/aata-files/aata-html/; item numbers as there).

## Definition

> [!definition] Parameters
> - $R$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
> - $S$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
> - $\varphi: R \to S$: a [[knowledge/math/set theory/Function\|Function]].

> [!definition] Ring Homomorphism
> Extends:: [[knowledge/math/property/map/Homomorphism\|Homomorphism]].
>
> ---
> Let $R, S$ be rings; a function $\varphi: R \rightarrow S$ is a ring homomorphism if:
> - Addition is preserved:
> $$(\forall a, b \in R): \varphi(a + b) = \varphi(a) + \varphi(b)$$
> - Multiplication is preserved:
> $$(\forall a, b \in R): \varphi(a b) = \varphi(a) \varphi(b)$$
> - Identity is preserved:
> $$\varphi(1_R) = 1_S$$
>
> `[Alu III.2.1]`

> [!remark] Convention: $\varphi(1_R) = 1_S$ is an axiom here
> `[Jud §16.3]` asks only that $\varphi$ preserve $+$ and $\cdot$; there $\varphi(1_R) = 1_S$ follows only when $\varphi$ is onto (`[Jud Prop 16.3.3]`). So the zero map $R \to S$ is a homomorphism in `[Jud]` but not here. The third axiom is what makes $\mathbb Z$ initial in [[knowledge/math/algebra/structures/ring/Category Ring\|Category Ring]] and rules out homomorphisms from the [[knowledge/math/algebra/structures/ring/example/Zero Ring\|Zero Ring]] to a nonzero ring.

### Kernel

Specializes [[knowledge/math/set theory/function/Kernel\|knowledge/math/set theory/function/Kernel]].

> [!definition] Parameters
> - $\varphi: R \to S$: a ring homomorphism.

> [!definition] Kernel
> The **kernel** of a homomorphism $\varphi: R \rightarrow S$ of [[knowledge/math/algebra/structures/ring/Ring\|Ring]] is
> $$\ker{\varphi} = \{r \in R \mid \varphi(r) = 0\}$$
>
> `[Alu III.3.1]` `[Jud §16.3]`

> [!proposition] Kernel is an ideal — $\ker \varphi$ is a two-sided ideal of $R$
> Let $\varphi: R \rightarrow S$ be any ring homomorphism. Then $\ker{\varphi}$ is an [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] of $R$.
>
> `[Alu III.3.1]` `[Jud Prop 16.3.8]`
>
> ---
> To be completed.

> [!theorem] Universal property of the quotient — a homomorphism with $I \subseteq \ker \varphi$ factors uniquely through $R/I$
> Let $I$ be a [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Two-sided Ideal]] of a [[knowledge/math/algebra/structures/ring/Ring\|Ring]] $R$. Then for every ring homomorphism $\varphi: R \rightarrow S$ such that $I \subseteq \ker \varphi$ there exists a unique ring homomorphism $\tilde{\varphi}: R / I \rightarrow S$ such that the diagram:
> $$\begin{CD}
> R @>\varphi>> S\\
> @| @AA\exists! \tilde{\varphi}A \\
> R @>>\pi> R/I
> \end{CD}$$
> commutes, where $\pi(r) = r + I$ is the [[knowledge/math/set theory/function/Canonical Projection\|Canonical Projection]] onto the [[knowledge/math/algebra/structures/ring/special ring/Quotient Ring\|Quotient Ring]] (`[Jud Thm 16.3.11]`).
>
> `[Alu III.3.2]`
>
> ---
> $\tilde{\varphi}(r + I) = \varphi(r)$.

## Property

### Ring Isomorphism

Specializes [[knowledge/math/algebra/category/Morphism#Isomorphism\|Isomorphism]].

> [!corollary] First isomorphism theorem — a surjective homomorphism gives $S \cong R / \ker \varphi$
> Suppose $\varphi: R \rightarrow S$ is a [[knowledge/math/property/map/Surjection\|Surjective]] ring homomorphism. Then
> $$S \cong \frac{R}{\ker{\varphi}}$$
>
> `[Alu III.3.3]` `[Jud Thm 16.3.12]`

> [!proposition] Third isomorphism theorem — $(R/I)/(J/I) \cong R/J$
> Let $I$ be an [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] of a ring $R$, and let $J$ be an ideal of $R$ containing $I$. Then $J / I$ is an ideal of $R / I$ and
> $$\frac{R/I}{J/I} \cong \frac{R}{J}.$$
>
> `[Alu III.3.3]` `[Jud Thm 16.3.14]`

### Ring Monomorphism

Specializes [[knowledge/math/algebra/category/Morphism#Monomorphism\|Monomorphism]].

> [!proposition] Monomorphisms are injections — mono, trivial kernel and injective are equivalent
> Let $\varphi: R \rightarrow S$ be a ring homomorphism, the following are equivalent:
> - $\varphi$ is a [[knowledge/math/algebra/category/Morphism#Monomorphism\|Monomorphism]].
> - $\mathrm{ker} \; \varphi = \{0\}$.
> - $\varphi$ is an [[knowledge/math/property/map/Injection\|Injection]].
>
> `[Alu III.2.3]`
>
> ---
> To be completed.

## Related

### Constructions
- [[knowledge/math/algebra/structures/ring/special ring/Quotient Ring\|Quotient Ring]] — $\pi: R \to R/I$, the homomorphism every factorization above goes through.
- [[knowledge/math/algebra/structures/ring/Category Ring\|Category Ring]] — rings and ring homomorphisms form $\mathsf{Ring}$.
- [[knowledge/math/algebra/structures/ring/module/R-algebra\|R-algebra]] — a ring homomorphism whose image lies in the [[knowledge/math/algebra/structures/ring/subring/Ring Center\|center]] of the target.

### Siblings
- [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] — the same notion for groups, where $\varphi(e) = e$ follows from the other axiom; the theorem shared across structures is [[knowledge/math/set theory/function/Canonical Decomposition\|Canonical Decomposition]].

### Prerequisites
- [[knowledge/math/algebra/structures/ring/Ring\|Ring]], [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]].
