---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/minimal-uncountable-well-ordered-set/","dg-note-properties":{"aliases":["S_Omega","SΩ","First Uncountable Ordinal"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §10: the corollary of the well-ordering theorem, Lemma 10.2, Theorem 10.3, Exercise 6; Supplementary Exercise 4(b) (Well-Ordering).
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, Theorem 2.12; Chapter 3, Lemma 3.4(i), read in the course copies: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf and https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/03-cardinal_numbers.pdf

## Intuition

> [!intuition] Why
> $S_\Omega$ is the smallest well-ordered set that cannot be listed as a sequence. Munkres uses it as a source of counterexamples: spaces in which every countable process stops short.

## Definition

> [!definition] Minimal Uncountable Well-Ordered Set
> Instantiates:: [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]]
>
> ---
> There is a [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]] $A$ with a largest element $\Omega$ such that the section $S_\Omega$ is uncountable and every other section of $A$ is [[knowledge/math/set theory/cardinality/Countable Set\|countable]] `[Mun00 Lemma 10.2]`. $S_\Omega$ is the **minimal uncountable well-ordered set**: it is uncountable, and every section of it is countable.

> [!remark] Unique up to order type
> Any two uncountable well-ordered sets whose sections are all countable have the same order type `[Mun00 Supp Ex 4b]`. In the language of ordinals ([[knowledge/math/set theory/order/Well-Ordered Set#Ordinals\|Well-Ordered Set#Ordinals]]), $S_\Omega$ is the least uncountable ordinal $\omega_1$.

## Property

> [!proof] Where it comes from
> Start from an uncountable well-ordered set $B$, which exists by the [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]] `[Mun00 §10 Cor]`. In $\{1, 2\} \times B$ with the [[knowledge/math/set theory/order/Dictionary Order\|Dictionary Order]], the section by any $(2, b)$ contains the uncountable set $\{1\} \times B$. Let $\Omega$ be the smallest element whose section is uncountable, and $A = S_\Omega \cup \{\Omega\}$.

> [!remark] Choice is more than needed
> Hartogs' construction gives, for every ordinal $\alpha$, an ordinal $h(\alpha)$ with $|\alpha| < |h(\alpha)|$ `[Jec03 Lemma 3.4(i)]`. Applied to $\omega$, it produces an uncountable well-ordered set without the [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]].

> [!theorem] Countable subsets are bounded — $S_\Omega$ is not exhausted in countably many steps
> **Scope**
> - $A \subseteq S_\Omega$ countable.
>
> ---
> **Property**
> $A$ has an upper bound in $S_\Omega$ `[Mun00 Thm 10.3]`.
>
> $\bigcup_{a \in A} S_a$ is a countable union of countable sets, hence countable ([[knowledge/math/set theory/cardinality/Countable Set#Property\|Countable Set#Property]]), so it is not all of $S_\Omega$. Any $x$ outside it satisfies $a \leq x$ for every $a \in A$. The countable-union step uses countably many choices.

> [!proposition] Long tails
> **Scope**
> - $S_\Omega$.
>
> ---
> **Property**
> $S_\Omega$ has no largest element.
> For every $a \in S_\Omega$, the set $\{x : a < x\}$ is uncountable.
> The set of $x \in S_\Omega$ with no immediate predecessor is uncountable.
>
> `[Mun00 §10 Ex 6]`

## Example

> [!example] Countable well-orders sit inside it
> $\mathbb Z_{>0}$, $\mathbb Z_{>0} \times \mathbb Z_{>0}$ in the dictionary order, and every countable well-ordered set have the order type of a section of $S_\Omega$. By [[knowledge/math/set theory/order/Well-Ordered Set#Comparability\|Well-Ordered Set#Comparability]] the only alternatives are $W \cong S_\Omega$ or $S_\Omega \cong$ a section of $W$, and both would make $S_\Omega$ countable.

## Related

### Prerequisites
- [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]], [[knowledge/math/set theory/cardinality/Countable Set\|Countable Set]], [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]]
