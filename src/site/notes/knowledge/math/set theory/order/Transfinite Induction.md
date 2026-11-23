---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/transfinite-induction/","dg-note-properties":{"aliases":["Principle of Transfinite Induction","Strong Induction","Inductive Subset"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1: §4, Theorem 4.2 (strong induction); §10, Exercise 7.
- `[Dob18]` — E.-E. Doberkat, _Sets, the Axiom of Choice, and All That: A Tutorial_, 2018, Theorem 1.21: https://arxiv.org/pdf/1408.6475
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, Theorem 2.14, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf

## Intuition

> [!intuition] Why
> Ordinary induction proves a statement for 1, 2, 3, …; transfinite induction does the same along any well-ordering, including ones longer than every natural number. It is the proof method behind the well-ordering and comparability theorems.

## Definition

> [!theorem] Transfinite Induction — an inductive subset is everything
> ### Scope
> - $(J, <)$: a [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]], with sections $S_\alpha$.
> - $J_0 \subseteq J$: **inductive**, meaning $S_\alpha \subseteq J_0 \Rightarrow \alpha \in J_0$ for every $\alpha \in J$.
>
> ---
> ### Condition
> - None: there is no separate base case.
>
> ---
> ### Property
> $$J_0 = J.$$
>
> `[Mun00 §10 Ex 7]`, `[Dob18 Thm 1.21]`

## Property

> [!proof] Why — there is no least counterexample
> If $J \setminus J_0 \neq \emptyset$, it has a smallest element $\alpha$. Every $x < \alpha$ lies in $J_0$, so $S_\alpha \subseteq J_0$, so $\alpha \in J_0$: a contradiction.

> [!remark] The base case is inside the hypothesis
> For the smallest element $\alpha_0$ of $J$, $S_{\alpha_0} = \emptyset \subseteq J_0$, so inductiveness alone forces $\alpha_0 \in J_0$.

> [!remark] Ordinal form
> Over the ordinals, `[Jec03 Thm 2.14]` splits the hypothesis into three cases: $0 \in C$; $\alpha \in C \Rightarrow \alpha + 1 \in C$; and $\alpha \in C$ for every nonzero limit $\alpha$ whose predecessors all lie in $C$.

## Example

> [!example] Strong induction on $\mathbb Z_{>0}$
> For $J = \mathbb Z_{>0}$, $S_n = \{1, \dots, n - 1\}$ and the theorem is the **strong induction principle**: if $\{1, \dots, n - 1\} \subseteq A$ implies $n \in A$ for every $n$, then $A = \mathbb Z_{>0}$ `[Mun00 Thm 4.2]`. Ordinary [[knowledge/math/Proofs#Principle of Mathematical Induction\|induction]] is the case where only $n - 1 \in A$ is used.

> [!example] Without a well-ordering it fails
> In $\mathbb Z$ every section $S_\alpha$ is nonempty, so $J_0 = \emptyset$ is inductive, and $J_0 \neq \mathbb Z$.

## Related

### Siblings
- [[knowledge/math/set theory/order/Principle of Recursive Definition\|Principle of Recursive Definition]] — defines functions over the same sections that this theorem proves statements over

### Prerequisites
- [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]]
