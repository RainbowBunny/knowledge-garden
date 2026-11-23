---
{"dg-publish":true,"permalink":"/knowledge/math/property/map/monotonicity/","dg-note-properties":{"aliases":["Order-Preserving Map","Increasing Function","Monotone Map"]}}
---

Reference:
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, the paragraph after Definition 2.2 (order-preserving, increasing, isomorphism), read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3 (same order type).

## Definition

> [!definition] Monotonicity
> ### Scope
> A map $f : P \to Q$ between sets with [[knowledge/math/set theory/order/Strict Partial Order\|strict partial orders]] $<_P$ and $<_Q$.
>
> ---
> ### Property
> $f$ is **order-preserving** iff
> $$\forall x, y \in P: x <_P y \Rightarrow f(x) <_Q f(y)$$
>
> `[Jec03 Ch 2]`, which calls an order-preserving map between linear orders **increasing**.

> [!remark] The non-strict version
> For [[knowledge/math/set theory/order/Partial Order\|partial orders]] $\leq$ the condition $x \leq y \Rightarrow f(x) \leq f(y)$ is weaker: a constant map satisfies it, but is not order-preserving once $P$ has two comparable elements. Maps satisfying the non-strict condition are the morphisms when a poset is read as a category ([[knowledge/math/property/Math Properties MOC\|Math Properties MOC]], *Orders as categories*).

## Property

> [!proposition] On a total order — order-preserving maps are embeddings
> **Scope**
> - $f : P \to Q$ order-preserving, with $<_P$ a [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]].
>
> ---
> **Property**
> $f$ is injective.
> $f(x) <_Q f(y) \Rightarrow x <_P y$.
>
> If $x \neq y$, then $x < y$ or $y < x$ by [[knowledge/math/property/relation/Comparability\|Comparability]], so $f(x) \neq f(y)$ by [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]] of $<_Q$. If $f(x) < f(y)$, then $x \neq y$, and $y < x$ would give $f(y) < f(x)$, against [[knowledge/math/property/relation/Asymmetry\|Asymmetry]]; so $x < y$. Hence an order-preserving bijection between strict total orders is an [[knowledge/math/set theory/order/Order Isomorphism\|Order Isomorphism]].

## Example

> [!example] When the inverse is not order-preserving
> Let $P = \{a, b\}$ with the empty strict order and $Q = \{a, b\}$ with $a < b$. The identity $P \to Q$ is an order-preserving bijection, but its inverse sends $a < b$ to an incomparable pair. This is why `[Jec03 Ch 2]` asks both $f$ and $f^{-1}$ to be order-preserving in an isomorphism, while `[Mun00 §3]`, working with total orders only, asks it of $f$.

> [!example] Increasing functions on $\mathbb R$
> $x \mapsto x^3$ and $x \mapsto e^x$ are increasing. $x \mapsto x^2$ is not, though its restriction to $[0, \infty)$ is.

## Related

### Descendants
- [[knowledge/math/set theory/order/Order Isomorphism\|Order Isomorphism]] — bijective, with an order-preserving inverse

### Siblings
- [[knowledge/math/property/map/Homomorphism\|Homomorphism]] — the structure-preserving map of the operation family
