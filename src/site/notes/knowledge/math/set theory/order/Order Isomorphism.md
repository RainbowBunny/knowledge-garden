---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/order-isomorphism/","dg-note-properties":{"aliases":["Order Type","Same Order Type","Order-Isomorphic"]}}
---

Reference:
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2: the paragraph after Definition 2.2 (isomorphism), the sentence after Theorem 2.8 (order-type), read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3 (same order type); §10, Exercise 4(a).

## Intuition

> [!intuition] Why
> Two ordered sets that differ only in the names of their elements should count as the same. An order isomorphism makes that precise, and the order type is what remains once the names are forgotten.

## Definition

> [!definition] Order Isomorphism
> Extends:: [[knowledge/math/property/map/Monotonicity\|Monotonicity]]
>
> ---
> Let $(P, <_P)$ and $(Q, <_Q)$ carry [[knowledge/math/set theory/order/Strict Partial Order\|strict partial orders]]. An **order isomorphism** is a [[knowledge/math/property/map/Bijection\|Bijection]] $f : P \to Q$ such that $f$ and $f^{-1}$ are [[knowledge/math/property/map/Monotonicity\|order-preserving]]:
> $$x <_P y \iff f(x) <_Q f(y).$$
>
> `[Jec03 Ch 2]`

### Order type

> [!definition] Order Type
> $P$ and $Q$ **have the same order type** iff there is an order isomorphism $P \to Q$ `[Jec03 Ch 2]` `[Mun00 §3]`.

> [!remark] Munkres asks only that $f$ preserve order
> `[Mun00 §3]` defines "same order type" between simply ordered sets by an order-preserving bijection. For [[knowledge/math/set theory/order/Strict Total Order\|strict total orders]] the inverse is then automatically order-preserving ([[knowledge/math/property/map/Monotonicity#Property\|Monotonicity#Property]]); for partial orders it need not be ([[knowledge/math/property/map/Monotonicity#Example\|Monotonicity#Example]]).

## Property

> [!proposition] Same order type — an equivalence
> **Scope**
> - Sets $P$, $Q$, $R$ with strict partial orders.
>
> ---
> **Property**
> $P$ has the order type of $P$.
> If $P$ has the order type of $Q$, then $Q$ has the order type of $P$.
> If $P$ has the order type of $Q$ and $Q$ that of $R$, then $P$ has the order type of $R$.
>
> Identities, inverses and composites of order isomorphisms are order isomorphisms.

> [!proposition] Invariants — whatever is defined from the order alone
> **Scope**
> - $f : P \to Q$ an order isomorphism.
>
> ---
> **Property**
> $f$ carries smallest and largest elements, [[knowledge/math/set theory/order/Supremum\|suprema]] and infima, immediate successors and predecessors to the same things in $Q$.
> $P$ has the [[knowledge/math/property/relation/Least Upper Bound Property\|Least Upper Bound Property]] iff $Q$ does; $P$ is a [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]] iff $Q$ is.

## Example

> [!example] $(-1, 1)$ and $\mathbb R$
> $f(x) = x / (1 - x^2)$ is increasing, since $f'(x) = (1 + x^2)/(1 - x^2)^2 > 0$, and maps $(-1, 1)$ onto $\mathbb R$. So a bounded interval and the whole line have the same order type `[Mun00 §3]`.

> [!example] Not the same order type
> - $\mathbb Z_{>0}$ and $\mathbb Z$: the first has a smallest element, the second does not.
> - $\mathbb Z$ and $\mathbb Q$: every integer has an immediate successor, no rational does.
> - A simply ordered set fails to be well-ordered iff it contains a subset with the order type of the negative integers $\mathbb Z_{<0}$ `[Mun00 §10 Ex 4a]`.

## Related

### Properties
- [[knowledge/math/set theory/order/Well-Ordered Set#Comparability\|Well-Ordered Set#Comparability]] — between well-ordered sets an isomorphism, if any, is unique, and one of any two is isomorphic to the other or to a section of it

### Siblings
- [[knowledge/math/algebra/category/Morphism\|Morphism]] — the categorical notion; an order isomorphism is an isomorphism in the category of ordered sets and order-preserving maps
