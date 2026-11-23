---
{"dg-publish":true,"permalink":"/knowledge/math/property/relation/least-upper-bound-property/","dg-note-properties":{"aliases":["Least-Upper-Bound Property","LUB Property","Greatest Lower Bound Property","Linear Continuum"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1: §3 (least upper bound property, greatest lower bound property; Exercise 13); §4 (linear continuum); §10, Exercise 1.
- `[Leb]` — J. Lebl, _Basic Analysis I: Introduction to Real Analysis, Volume I_, §1.1: Definitions 1.1.2, 1.1.3, Example 1.1.4, Proposition 1.1.11: https://www.jirka.org/ra/html/sec_basicpropsrn.html

## Intuition

> [!intuition] Why
> This is completeness of an order: it has no gaps. It is the property of ℝ that makes limits, the intermediate value theorem and calculus work, and that ℚ lacks.

## Definition

> [!definition] Least Upper Bound Property
> ### Scope
> A [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] $<$ on a set $O$.
>
> ---
> ### Property
> $(O, <)$ has the **least upper bound property** iff every nonempty subset that is bounded above has a [[knowledge/math/set theory/order/Supremum\|supremum]]:
> $$\forall A \subseteq O: \big(A \neq \emptyset \land A \text{ bounded above}\big) \Rightarrow \sup A \text{ exists in } O$$
>
> `[Mun00 §3]`, `[Leb Def 1.1.3]`. The **greatest lower bound property** is the same with "bounded below" and $\inf$ `[Mun00 §3]`.

## Property

> [!theorem] LUB implies GLB — an infimum is the supremum of the lower bounds
> **Scope**
> - $(O, <)$ with the least upper bound property.
> - $B \subseteq O$ nonempty and bounded below; $L$ the set of its lower bounds.
>
> ---
> **Property**
> $\sup L$ exists.
> $$\inf B = \sup L.$$
> So $(O, <)$ has the greatest lower bound property.
>
> `[Mun00 §3 Ex 13]`. `[Leb Prop 1.1.11]` proves the case of an ordered field, by negating.

> [!proof] Why
> $L \neq \emptyset$ because $B$ is bounded below. Every $b \in B$ is an upper bound of $L$, and $B \neq \emptyset$, so $L$ is bounded above; let $\alpha = \sup L$. Each $b \in B$ is an upper bound of $L$, so $\alpha \leq b$: $\alpha$ is a lower bound of $B$. Every lower bound $\ell \in L$ satisfies $\ell \leq \alpha$, since $\alpha$ is an upper bound of $L$. So $\alpha$ is the greatest lower bound of $B$.

## Variant

Adding density to the least upper bound property gives the ordered sets that behave like $\mathbb R$.

### Linear continuum

> [!definition] Linear Continuum
> A [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] $(L, <)$ is a **linear continuum** iff
> - it has the least upper bound property;
> - between any two elements there is a third: $x < y \Rightarrow \exists z: x < z < y$.
>
> `[Mun00 §4]`, where these are among the order properties assumed of $\mathbb R$.

## Example

> [!example] Where it holds and where it fails
> - $\mathbb R$ has it: it is the [[knowledge/math/calculus/Real Number#Bound\|least-upper-bound axiom]]. $\mathbb R$ is a linear continuum, and so is every open interval $(a, b)$ of it.
> - $\mathbb Q$ does not: $\{x \in \mathbb Q : x^2 < 2\}$ is bounded above with no supremum in $\mathbb Q$ `[Leb Ex 1.1.4]`.
> - Every [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]] has it `[Mun00 §10 Ex 1]`: the supremum is the least element of the nonempty set of upper bounds.
> - $\mathbb Z$ has it but is not a linear continuum: nothing lies strictly between $0$ and $1$.

## Related

### Prerequisites
- [[knowledge/math/set theory/order/Supremum\|Supremum]], [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]]

### Siblings
- [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]] — every nonempty subset has a least element; a well-ordered set has the least upper bound property, and $\mathbb R$ shows the converse fails
