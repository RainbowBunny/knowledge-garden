---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/principle-of-recursive-definition/","dg-note-properties":{"aliases":["Recursion Theorem","Transfinite Recursion","Recursion Formula","General Principle of Recursive Definition"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1: §7, Lemma 7.2; §8: Lemmas 8.1, 8.2, Theorems 8.3, 8.4; §10, Exercise 10; Supplementary Exercise 1 (Well-Ordering).
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, Theorem 2.15, Corollary 2.16, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf

## Intuition

> [!intuition] Why
> Recursive definitions, defining $h(n)$ from the earlier values, are everywhere: factorials, sequences, listing an infinite set. This theorem guarantees that such a definition determines exactly one function, which is not obvious from the formula alone.

## Definition

> [!theorem] Principle of Recursive Definition — a recursion formula has exactly one solution
> ### Scope
> - $A$: a set; $a_0 \in A$.
> - $\rho$: a function assigning to each function $f$ from a nonempty section $\{1, \dots, n\}$ of $\mathbb Z_{>0}$ into $A$ an element $\rho(f) \in A$.
>
> ---
> ### Condition
> - None.
>
> ---
> ### Property
> There is a unique function $h : \mathbb Z_{>0} \to A$ with
> $$h(1) = a_0,$$
> $$h(i) = \rho\big(h|_{\{1, \dots, i - 1\}}\big) \text{ for } i > 1.$$
>
> `[Mun00 Thm 8.4]`. The two equations are a **recursion formula** for $h$: they give $h(1)$, and $h(i)$ in terms of the values of $h$ below $i$.

## Property

> [!proof] Why — glue the partial solutions
> 1. For each $n$ there is a function on $\{1, \dots, n\}$ satisfying the formula wherever it is defined, by induction on $n$ `[Mun00 Lemma 8.1]`.
> 2. Two such partial functions agree on their common domain, by induction `[Mun00 Lemma 8.2]`.
> 3. Their union is a function on $\mathbb Z_{>0}$ satisfying the formula, and it is the only one `[Mun00 Thm 8.3]`.
>
> `[Mun00 §8]` carries out 1–3 for the formula of the first example below, then states the general theorem with the same proof.

### General form

> [!theorem] General Principle of Recursive Definition — recursion over a well-ordered set
> **Scope**
> - $(J, <)$: a [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]] with sections $S_\alpha$; $C$: a set.
> - $\mathcal F$: the set of functions from sections of $J$ into $C$; $\rho : \mathcal F \to C$.
>
> ---
> **Property**
> There is a unique $h : J \to C$ with
> $$h(\alpha) = \rho\big(h|_{S_\alpha}\big) \text{ for every } \alpha \in J.$$
>
> `[Mun00 Supp Ex 1]`. The proof is the same, with [[knowledge/math/set theory/order/Transfinite Induction\|Transfinite Induction]] in place of induction. No $a_0$ is needed: at the smallest element $S_\alpha = \emptyset$, and $h(\alpha) = \rho(\emptyset)$. `[Jec03 Thm 2.15]` is the version over the class of ordinals, and `[Jec03 Cor 2.16]` the version up to a given ordinal.

## Example

> [!example] Listing an infinite subset of $\mathbb Z_{>0}$
> For an infinite $C \subseteq \mathbb Z_{>0}$, the formula
> $$h(1) = \text{smallest element of } C,$$
> $$h(i) = \text{smallest element of } C \setminus h(\{1, \dots, i - 1\}) \text{ for } i > 1$$
> has a unique solution $h : \mathbb Z_{>0} \to C$ `[Mun00 Thm 8.3]`, and $h$ is a bijection, so $C$ is countably infinite `[Mun00 Lemma 7.2]` ([[knowledge/math/set theory/cardinality/Countable Set\|Countable Set]]). The set $C \setminus h(\{1, \dots, i - 1\})$ is nonempty because $C$ is infinite, and its smallest element exists because $\mathbb Z_{>0}$ is well-ordered: no choice is made.

> [!example] The same formula over a well-ordered set
> For well-ordered $J$ and $C$ such that no section of $J$ maps onto $C$, $h(x) = \text{smallest}\,[C \setminus h(S_x)]$ has a unique solution $h : J \to C$ `[Mun00 §10 Ex 10]`. It is injective, since $h(x) \notin h(S_x)$. This is the step behind [[knowledge/math/set theory/cardinality/Cardinality#Comparability of cardinals\|Cardinality#Comparability of cardinals]] and [[knowledge/math/set theory/order/Well-Ordered Set#Comparability\|Well-Ordered Set#Comparability]].

> [!example] Factorial
> With $a_0 = 1$ and $\rho(f) = (n + 1)\, f(n)$ for $f$ defined on $\{1, \dots, n\}$, the solution is $h(i) = i!$.

## Related

### Siblings
- [[knowledge/math/set theory/order/Transfinite Induction\|Transfinite Induction]] — proves statements over the sections that this theorem defines functions over

### Prerequisites
- [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]]
