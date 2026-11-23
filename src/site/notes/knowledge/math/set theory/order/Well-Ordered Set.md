---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/well-ordered-set/","dg-note-properties":{"aliases":["Well-Ordering","Well-Order","Initial Segment","Section of a Well-Ordered Set"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1: §4, Theorem 4.1; §10: definition, Theorem 10.1, section $S_\alpha$, Exercises 1, 2(a), 4(a), 9; Supplementary Exercises 2, 4 (Well-Ordering).
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2: Definition 2.3, Lemma 2.4, Corollaries 2.5, 2.6, initial segment, Lemma 2.7, Theorems 2.8, 2.12, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf
- `[Dob18]` — E.-E. Doberkat, _Sets, the Axiom of Choice, and All That: A Tutorial_, 2018, Definition 1.10: https://arxiv.org/pdf/1408.6475
- `[Nor12]` — D. Normann, _The Axiom of Choice, the Well Ordering Principle and Zorn's Lemma_, note for MAT4640, University of Oslo, 2012, §2 (definitions), Lemma 6(b): https://www.uio.no/studier/emner/matnat/math/MAT4640/v14/acwozl.pdf

## Intuition

> [!intuition] Why
> In a well-ordered set every nonempty subset has a first element. That is what makes induction work, and it carries induction and recursion beyond the natural numbers to any well-ordered set.

## Definition

> [!definition] Well-Ordered Set
> Extends:: [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]]
>
> ---
> A **well-ordered set** is a set $A$ with a [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] $<$ in which every nonempty subset has a smallest element:
> $$\forall C \subseteq A: C \neq \emptyset \Rightarrow \exists c \in C\; \forall x \in C: c \leq x.$$
> The order $<$ is then a **well-ordering** of $A$.
>
> `[Mun00 §10]`, `[Jec03 Def 2.3]`, `[Dob18 Def 1.10]`, `[Nor12 §2]`

### Sections

> [!definition] Section
> For $\alpha \in A$, the **section** of $A$ by $\alpha$ is
> $$S_\alpha = \{x \in A : x < \alpha\}.$$
>
> `[Mun00 §10]`; `[Jec03 Ch 2]` calls it the **initial segment** given by $\alpha$.

## Property

> [!proposition] Subsets and finite sets
> **Scope**
> - $(A, <)$ well-ordered and $B \subseteq A$.
> - $F$ a nonempty finite simply ordered set.
>
> ---
> **Property**
> $B$ is well-ordered by the restriction of $<$.
> $F$ has the order type of a section $\{1, \dots, n\}$ of $\mathbb Z_{>0}$, so it is well-ordered `[Mun00 Thm 10.1]`.

> [!proposition] Successors and suprema
> **Scope**
> - $(A, <)$ well-ordered.
>
> ---
> **Property**
> Every element except the largest, if there is one, has an immediate successor `[Mun00 §10 Ex 2a]`: the smallest element of $\{x : \alpha < x\}$.
> $A$ has the [[knowledge/math/property/relation/Least Upper Bound Property\|Least Upper Bound Property]] `[Mun00 §10 Ex 1]`: the supremum of a nonempty bounded-above set is the smallest of its upper bounds.

> [!proposition] Descending sequences — the obstruction to well-ordering
> **Scope**
> - $(A, <)$ a [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]].
>
> ---
> **Property**
> $A$ is well-ordered iff it contains no subset with the order type of the negative integers $\mathbb Z_{<0}$ `[Mun00 §10 Ex 4a]`.
>
> Such a subset is a sequence $a_1 > a_2 > \cdots$ with no smallest element. Conversely, a nonempty subset with no smallest element lets one pick $a_{n+1} < a_n$ for ever, one choice at each step.

### Comparability

> [!lemma] Increasing self-maps — never move an element down
> **Scope**
> - $(W, <)$ well-ordered; $f : W \to W$ [[knowledge/math/property/map/Monotonicity\|increasing]].
>
> ---
> **Property**
> $f(x) \geq x$ for every $x \in W$.
>
> `[Jec03 Lemma 2.4]`. Otherwise let $x$ be the least element with $f(x) < x$; then $f(f(x)) < f(x)$, so $f(x)$ is a smaller one.

> [!corollary] Rigidity — isomorphisms between well-orders are unique
> **Scope**
> - $W_1$, $W_2$ well-ordered.
>
> ---
> **Property**
> The only automorphism of $W_1$ is the identity `[Jec03 Cor 2.5]`.
> If $W_1$ and $W_2$ are isomorphic, the [[knowledge/math/set theory/order/Order Isomorphism\|Order Isomorphism]] between them is unique `[Jec03 Cor 2.6]`.
> $W_1$ is not isomorphic to any of its sections `[Jec03 Lemma 2.7]`.
> Distinct sections of $W_1$ have distinct order types `[Mun00 Supp Ex 2b]`.
>
> An isomorphism $f : W \to S_u$ would have $f(u) < u$, against the lemma; and if $\alpha < \beta$, $S_\alpha$ is a section of $S_\beta$.

> [!theorem] Comparability of Well-Orders — one is a section of the other
> **Scope**
> - $W_1$, $W_2$: well-ordered sets.
>
> ---
> **Property**
> Exactly one of the following holds:
> - $W_1$ is isomorphic to $W_2$;
> - $W_1$ is isomorphic to a section of $W_2$;
> - $W_2$ is isomorphic to a section of $W_1$.
>
> `[Jec03 Thm 2.8]`, `[Nor12 Lemma 6(b)]`. `[Mun00 Supp Ex 4a]` builds it from the [[knowledge/math/set theory/order/Principle of Recursive Definition#General form\|general recursion theorem]].

> [!proof] Why
> Let $f$ be the set of pairs $(x, y) \in W_1 \times W_2$ such that the section of $W_1$ by $x$ is isomorphic to the section of $W_2$ by $y$. By rigidity, $f$ is an injective function; it is order-preserving; its domain is $W_1$ or a section of $W_1$, and its range is $W_2$ or a section of $W_2$. If both were proper sections, by $x$ and by $y$, then $(x, y) \in f$, which is impossible. At most one case holds, again by rigidity. `[Jec03 Thm 2.8]`

### Ordinals

> [!remark] Canonical representatives
> Every well-ordered set is isomorphic to a unique ordinal `[Jec03 Thm 2.12]`, so the ordinals are canonical representatives of the order types of well-ordered sets.

## Example

> [!example] Well-ordered and not
> - $\mathbb Z_{>0}$ under $<$ is well-ordered: the well-ordering property `[Mun00 Thm 4.1]`, the [[knowledge/math/Proofs#Principle of Mathematical Induction\|well-ordering principle]].
> - $\mathbb Z_{>0} \times \mathbb Z_{>0}$ in the [[knowledge/math/set theory/order/Dictionary Order\|Dictionary Order]] is well-ordered, and so is the antidictionary order of `[Mun00 §10 Ex 9]`.
> - $\mathbb Z$, $\mathbb Q_{\geq 0}$, $[0, 1]$ under $<$ are not: $\mathbb Z_{<0}$, $\{1/n : n \geq 1\}$ and $(0, 1]$ have no smallest element.
> - $\mathbb Z_{>0}$ under $>$ is not: the whole set has no smallest element.
> - Every set has some well-ordering by the [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]], which is equivalent to the [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]].

## Related

### Instantiations
- [[knowledge/math/set theory/order/Minimal Uncountable Well-Ordered Set\|Minimal Uncountable Well-Ordered Set]] — $S_\Omega$: uncountable, with every section countable

### Properties
- [[knowledge/math/set theory/order/Transfinite Induction\|Transfinite Induction]] — proofs over sections
- [[knowledge/math/set theory/order/Principle of Recursive Definition\|Principle of Recursive Definition]] — definitions over sections
- [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]] — every set has a well-ordering

### Siblings
- [[knowledge/math/property/relation/Least Upper Bound Property\|Least Upper Bound Property]] — implied by well-ordering; $\mathbb R$ has it and is not well-ordered
- [[knowledge/math/algebra/structures/polynomial/monomial order/Monomial Order\|Monomial Order]] — a total order on monomials that is a well-ordering
