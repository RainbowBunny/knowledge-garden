---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/choice/well-ordering-theorem/","dg-note-properties":{"aliases":["Zermelo's Well-Ordering Theorem","WOT"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §10: the well-ordering theorem and its corollary; Exercises 5, 11; Supplementary Exercises 6, 7 (Well-Ordering).
- `[Dob18]` — E.-E. Doberkat, _Sets, the Axiom of Choice, and All That: A Tutorial_, 2018, Proposition 1.17, Theorem 1.40, Theorem 1.45: https://arxiv.org/pdf/1408.6475
- `[Nor12]` — D. Normann, _The Axiom of Choice, the Well Ordering Principle and Zorn's Lemma_, note for MAT4640, University of Oslo, 2012, Theorems 5, 10: https://www.uio.no/studier/emner/matnat/math/MAT4640/v14/acwozl.pdf
- `[Reed]` — _The Axiom of Choice, Zorn's Lemma, and the Well Ordering Principle_, Reed College Math 332 notes, after van der Waerden, Theorem 5.1: https://people.reed.edu/~jerry/332/23zorn.pdf

## Intuition

> [!intuition] Why
> If every set can be well-ordered, induction and recursion work on every set. That is the use of this theorem: it makes transfinite arguments available everywhere, at the price of the axiom of choice.

## Definition

> [!theorem] Well-Ordering Theorem — every set can be well-ordered
> ### Scope
> - $A$: a set.
>
> ---
> ### Condition
> - The [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]], to which the theorem is equivalent.
>
> ---
> ### Property
> There is an order relation on $A$ that is a [[knowledge/math/set theory/order/Well-Ordered Set\|well-ordering]].
>
> `[Mun00 §10]`, `[Dob18 Thm 1.45 (WO)]`, `[Nor12 WO]`, `[Reed Thm 5.1]`

## Property

> [!proof] Well-ordering ⇒ choice
> Given a collection $\mathcal B$ of nonempty sets, well-order $\bigcup \mathcal B$ and let $c(B)$ be the smallest element of $B$ `[Mun00 §10 Ex 5]` `[Dob18 Prop 1.17]`.

> [!proof] Choice ⇒ well-ordering, in outline `[Reed Thm 5.1]`
> Fix a choice function $\varphi$ giving each proper subset $S \subsetneq A$ an element $\varphi(S) \in A \setminus S$. Call a well-ordered subset $W \subseteq A$ a $\varphi$-chain if each $t \in W$ is $\varphi$ of its own section: $t = \varphi(S_t)$. Any two $\varphi$-chains are comparable, one being equal to the other or a section of it, so their union $U$ is again a $\varphi$-chain. If $U \neq A$, putting $\varphi(U)$ on top gives a larger $\varphi$-chain; hence $U = A$. `[Dob18 Thm 1.40]` and `[Nor12 Thm 10]` prove the same implication.

> [!corollary] An uncountable well-ordered set exists
> Well-order any uncountable set, such as $\mathbb R$ `[Mun00 §10]`. This is the starting point of the [[knowledge/math/set theory/order/Minimal Uncountable Well-Ordered Set\|Minimal Uncountable Well-Ordered Set]].

> [!corollary] Cardinals are comparable
> Any two sets satisfy $|A| \leq |B|$ or $|B| \leq |A|$ `[Mun00 §10 Ex 11]`; see [[knowledge/math/set theory/cardinality/Cardinality#Comparability of cardinals\|Cardinality#Comparability of cardinals]].

## Example

> [!example] Sets with an explicit well-ordering
> Finite sets, $\mathbb Z_{>0}$ in its usual order, $\mathbb Z$ listed as $0, 1, -1, 2, -2, \dots$, and every countable set, by pulling back the order of $\mathbb Z_{>0}$ along a bijection. For uncountable sets such as $\mathbb R$ this method is not available, and the theorem supplies the well-ordering.

## Related

### Siblings
- [[knowledge/math/set theory/choice/Zorn's Lemma\|Zorn's Lemma]], [[knowledge/math/set theory/choice/Hausdorff Maximum Principle\|Hausdorff Maximum Principle]] — the other equivalents of choice
- [[knowledge/math/Proofs#Principle of Mathematical Induction\|Well-ordering principle]] — the fact that the usual order of $\mathbb Z_{>0}$ is a well-ordering, which needs no choice

### Prerequisites
- [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]], [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]]
