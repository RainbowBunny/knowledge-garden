---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/supremum/","dg-note-properties":{"aliases":["Least Upper Bound","Infimum","Greatest Lower Bound","Upper Bound","Lower Bound","Bounded Above","Bounded Below"]}}
---

Reference:
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, Definition 2.2, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf
- `[Leb]` — J. Lebl, _Basic Analysis I: Introduction to Real Analysis, Volume I_, §1.1: Definition 1.1.2 and the remark after it, Example 1.1.4, Exercise 1.1.5: https://www.jirka.org/ra/html/sec_basicpropsrn.html
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3.

## Intuition

> [!intuition] Why
> The supremum is the best possible upper bound. It need not belong to the set, as $1 = \sup\,(0, 1)$, and whether it always exists is exactly what separates ℝ from ℚ.

## Definition

> [!definition] Parameters
> - $(O, <)$: a set with a [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]]; $x \leq y$ means $x < y$ or $x = y$.
> - $A \subseteq O$.

> [!definition] Upper Bound and Lower Bound
> - $b \in O$ is an **upper bound** of $A$ iff $x \leq b$ for every $x \in A$; $A$ is **bounded above** iff it has one.
> - $b \in O$ is a **lower bound** of $A$ iff $b \leq x$ for every $x \in A$; $A$ is **bounded below** iff it has one.
>
> `[Jec03 Def 2.2]`, `[Leb Def 1.1.2]`, `[Mun00 §3]`

> [!definition] Supremum
> - The **supremum** (least upper bound) $\sup A$ is the least element of the set of upper bounds of $A$, if that set has one.
> - The **infimum** (greatest lower bound) $\inf A$ is the greatest element of the set of lower bounds of $A$, if that set has one.
>
> `[Jec03 Def 2.2]`, `[Leb Def 1.1.2]`, `[Mun00 §3]`

## Property

> [!proposition] Uniqueness — a set has at most one supremum
> **Scope**
> - $A \subseteq O$.
>
> ---
> **Property**
> If $b$ and $b'$ are suprema of $A$, then $b = b'$.
>
> Each is $\leq$ the other, and $\leq$ is antisymmetric `[Leb]`, remark after Def 1.1.2.

> [!proposition] Largest element — a supremum inside the set
> **Scope**
> - $A \subseteq O$ and $g \in A$ an upper bound of $A$, i.e. the largest element of $A$.
>
> ---
> **Property**
> $\sup A = g$.
>
> Any upper bound $b$ satisfies $g \leq b$ because $g \in A$ `[Leb Ex 1.1.5]`.

> [!remark] The empty set
> Every element of $O$ is an upper bound of $\emptyset$, so $\sup \emptyset$ is the least element of $O$ when there is one, and does not exist otherwise. This is why the [[knowledge/math/property/relation/Least Upper Bound Property\|Least Upper Bound Property]] asks only about nonempty sets.

## Example

> [!example] Inside and outside the set
> - In $\mathbb R$: $\sup\, (0, 1) = 1 \notin (0, 1)$, while $\sup\, [0, 1] = 1$ is the largest element.
> - In $\mathbb Q$: $\{x \in \mathbb Q : x^2 < 2\}$ is bounded above and has no supremum `[Leb Ex 1.1.4]`.
> - In $\mathcal P(X)$ under $\subsetneq$: $\sup \{A, B\} = A \cup B$ and $\inf \{A, B\} = A \cap B$.

## Related

### Properties
- [[knowledge/math/property/relation/Least Upper Bound Property\|Least Upper Bound Property]] — every nonempty bounded-above subset has a supremum

### Siblings
- [[knowledge/math/set theory/order/Strict Partial Order#Upper bounds and maximal elements\|Strict Partial Order#Upper bounds and maximal elements]] — a maximal element has nothing above it, which is weaker than lying above everything
