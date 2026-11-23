---
{"dg-publish":true,"permalink":"/knowledge/math/topology/convergent-sequence/","dg-note-properties":{"aliases":["Convergence of a Sequence","Limit of a Sequence","Converges"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §17: convergence of sequences, Theorem 17.10; §19, Exercise 6.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, p. 6: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf

## Intuition

> [!intuition] Why
> Convergence is the familiar way of saying that points get arbitrarily close. In a general space it can misbehave, with one sequence converging to several points, and seeing when this happens motivates the Hausdorff condition.

## Definition

> [!definition] Convergent Sequence
> A sequence $x_1, x_2, \dots$ of points of a [[knowledge/math/topology/Topological Space\|Topological Space]] $X$ **converges** to $x \in X$ iff for every [[knowledge/math/topology/Closure and Interior\|neighborhood]] $U$ of $x$ there is $N \in \mathbb Z_{>0}$ with $x_n \in U$ for all $n \geq N$.
>
> `[Mun00 §17]`; `[Hat p. 6]`: $x_n \in U$ for all but finitely many $n$.

## Property

> [!theorem] Uniqueness of limits — in a Hausdorff space
> **Scope**
> - $X$ a [[knowledge/math/topology/Hausdorff Space\|Hausdorff Space]].
>
> ---
> **Property**
> A sequence in $X$ converges to at most one point.
>
> `[Mun00 Thm 17.10]`. If $x_n \to x$ and $x_n \to y \neq x$, take disjoint neighborhoods $U \ni x$, $V \ni y$; from some index on $x_n$ lies in both.

> [!remark] Sequences do not see the topology
> In $\mathbb R^n$ a limit point of $A$ is the limit of a sequence of points of $A$, but not in an arbitrary space `[Hat p. 6]`. Sequences describe closures only under a countability condition, which Munkres treats later.

## Example

> [!example] Where limits are not unique
> - Trivial topology: the only neighborhood of any point is $X$, so every sequence converges to every point.
> - Finite complement topology on an infinite set: a sequence of distinct points converges to every point, since a neighborhood misses only finitely many points.
> - In $\mathbb R$, $1/n \to 0$, and $0$ is the only limit.
> - In a product with the product topology, a sequence converges iff every coordinate sequence does `[Mun00 §19 Ex 6]` ([[knowledge/math/topology/Product Topology#Box versus product\|Product Topology#Box versus product]]).

## Related

### Siblings
- [[knowledge/math/topology/Limit Point\|Limit Point]] — a property of a set, not of a sequence

### Prerequisites
- [[knowledge/math/topology/Topological Space\|Topological Space]]
