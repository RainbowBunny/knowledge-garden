---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/choice/hausdorff-maximum-principle/","dg-note-properties":{"aliases":["Maximum Principle","Hausdorff Maximality Principle","Hausdorff Maximal Principle"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §11: the maximum principle; Exercise 7; Supplementary Exercises 5, 6 (Well-Ordering).
- `[Ros88]` — K. A. Ross, _Informal Introduction to Set Theory_, lecture notes, University of Oregon, 1988, Hausdorff Maximality Principle (unnumbered): https://people.iith.ac.in/rajeshkannan/ra2021/axiomofchoice.pdf

## Intuition

> [!intuition] Why
> The maximum principle produces a maximal chain in any partial order, and Zorn's lemma follows by taking an upper bound of that chain. It is the step between choice and the maximality arguments.

## Definition

> [!theorem] Hausdorff Maximum Principle — every strict partial order has a maximal chain
> ### Scope
> - $(A, \prec)$: a set with a [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]].
>
> ---
> ### Condition
> - The [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]], to which it is equivalent.
>
> ---
> ### Property
> There is a maximal simply ordered subset $B \subseteq A$: a chain contained in no strictly larger chain.
>
> `[Mun00 §11]` ("the maximum principle"); `[Ros88]` ("Hausdorff Maximality Principle", for nonempty partially ordered sets).

## Property

> [!remark] How it connects to the other equivalents
> | implication | where |
> | --- | --- |
> | maximum principle ⇒ [[knowledge/math/set theory/choice/Zorn's Lemma\|Zorn's Lemma]] | `[Mun00 §11]`, in the text ([[knowledge/math/set theory/choice/Zorn's Lemma#Property\|Zorn's Lemma#Property]]) |
> | Tukey's lemma ⇒ maximum principle | `[Mun00 §11 Ex 7]` |
> | maximum principle ⇔ [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]] | `[Mun00 Supp Ex 6]` |
> | AC ⇒ maximum principle | `[Ros88]`, through Bourbaki's fixed point theorem |

> [!proof] Tukey ⇒ maximum principle `[Mun00 §11 Ex 7]`
> Let $\mathcal A$ be the collection of chains of $(A, \prec)$. A subset is a chain iff each of its two-element subsets is, hence iff each of its finite subsets is: $\mathcal A$ is of finite type, and it contains $\emptyset$. A maximal member of $\mathcal A$, given by [[knowledge/math/set theory/choice/Zorn's Lemma#Tukey's lemma\|Tukey's lemma]], is a maximal chain.

> [!remark] Toward the well-ordering theorem
> `[Mun00 Supp Ex 5]` orders the pairs $(B, <)$ with $B \subseteq X$ and $<$ a well-ordering of $B$ by "is a section of", and shows that the union of a chain of such pairs is again well-ordered. A maximal chain then yields a well-ordered subset that cannot be extended, which must be all of $X$: the maximum principle implies the well-ordering theorem.

## Example

> [!example] Maximal chains
> - In $\mathcal P(\{1, 2, 3\})$ under $\subsetneq$, $\emptyset \subsetneq \{1\} \subsetneq \{1, 2\} \subsetneq \{1, 2, 3\}$ is a maximal chain; there are $3! = 6$ of them, one for each order of adding the elements.
> - In a [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] the whole set is the only maximal chain; for $\mathbb Z_{>0}$ under $<$ it has no largest element.

## Related

### Siblings
- [[knowledge/math/set theory/choice/Zorn's Lemma\|Zorn's Lemma]] — a maximal element instead of a maximal chain
- [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]], [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]]
