---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/dictionary-order/","dg-note-properties":{"aliases":["Dictionary Order Relation","Lexicographic Order","Antidictionary Order"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3 (dictionary order relation); §10, Exercise 9 (antidictionary order).

## Intuition

> [!intuition] Why
> The dictionary order is the standard way to order pairs, words and tuples. It builds new ordered sets from old ones, such as the ordered square, and it is the lexicographic monomial order behind Gröbner bases.

## Definition

> [!definition] Parameters
> - $(A, <_A)$, $(B, <_B)$: sets with [[knowledge/math/set theory/order/Strict Total Order\|strict total orders]].

> [!definition] Dictionary Order
> The **dictionary order** on the [[knowledge/math/set theory/Set Operation#Cartesian Product\|cartesian product]] $A \times B$ is
> $$(a_1, b_1) < (a_2, b_2) \iff a_1 <_A a_2 \;\lor\; (a_1 = a_2 \land b_1 <_B b_2).$$
>
> `[Mun00 §3]`. The first coordinates are compared, and the second ones only break a tie.

## Property

> [!proposition] Dictionary Order — a strict total order
> **Scope**
> - $<_A$, $<_B$ strict total orders.
>
> ---
> **Property**
> The dictionary order is a [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] on $A \times B$.
>
> Irreflexive: neither disjunct holds for a pair and itself. Comparable: if $(a_1, b_1) \neq (a_2, b_2)$, either $a_1 \neq a_2$, decided by $<_A$, or $a_1 = a_2$ and $b_1 \neq b_2$, decided by $<_B$. Transitive: by cases on which first coordinates are equal.

> [!proposition] Products of well-orders — well-ordered
> **Scope**
> - $<_A$, $<_B$ well-orderings.
>
> ---
> **Property**
> $A \times B$ in the dictionary order is a [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]].
>
> For nonempty $C \subseteq A \times B$, let $a_0$ be the least first coordinate of an element of $C$, and $b_0$ the least $b$ with $(a_0, b) \in C$. Then $(a_0, b_0)$ is the least element of $C$.

## Example

> [!example] The ordered square and two copies of $\mathbb Z_{>0}$
> - $\mathbb R \times \mathbb R$: $(1, 5) < (2, 0)$ because $1 < 2$, and $(1, 0) < (1, 5)$.
> - $\{1, 2\} \times \mathbb Z_{>0}$: every element of $\{1\} \times \mathbb Z_{>0}$ lies below every element of $\{2\} \times \mathbb Z_{>0}$. The element $(2, 1)$ is not the smallest and has no immediate predecessor, so this set does not have the [[knowledge/math/set theory/order/Order Isomorphism\|order type]] of $\mathbb Z_{>0}$, where every element but $1$ has one.
> - In $\mathbb Z_{>0} \times \mathbb Z_{>0}$ the elements $(n, 1)$ with $n \geq 2$ have no immediate predecessor.

> [!example] Antidictionary order `[Mun00 §10 Ex 9]`
> On the sequences $x = (x_1, x_2, \dots)$ of positive integers that end in an infinite string of $1$s, set $x < y$ iff for some $n$, $x_n < y_n$ and $x_i = y_i$ for all $i > n$: compare at the last place where they differ. The exercise shows that this set is well-ordered and that for every $n$ some section of it has the order type of $(\mathbb Z_{>0})^n$ in the dictionary order.

## Related

### Constructions
- [[knowledge/math/topology/Order Topology\|Order Topology]] — the dictionary order topology; on $I \times I$ it is the ordered square

### Siblings
- [[knowledge/math/algebra/structures/polynomial/monomial order/example/Lexicographic Monomial Order\|Lexicographic Monomial Order]] — the $n$-fold dictionary order on exponent vectors in $\mathbb Z_{\geq 0}^n$

### Prerequisites
- [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]], [[knowledge/math/set theory/Set Operation#Cartesian Product\|Set Operation#Cartesian Product]]
