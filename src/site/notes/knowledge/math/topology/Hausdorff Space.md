---
{"dg-publish":true,"permalink":"/knowledge/math/topology/hausdorff-space/","dg-note-properties":{"aliases":["T2 Space","Hausdorff"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §17: Hausdorff spaces, Theorems 17.8, 17.10, 17.11; §19, Theorem 19.4.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 30–31: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf

## Intuition

> [!intuition] Why
> In a Hausdorff space open sets can tell points apart, which makes limits unique and points closed, as in every metric space. Almost every space used in analysis is Hausdorff; those that are not, like the Zariski topology, need separate care.

## Definition

> [!definition] Hausdorff Space
> Extends:: [[knowledge/math/topology/Topological Space\|Topological Space]]
>
> ---
> A **Hausdorff space** is a [[knowledge/math/topology/Topological Space\|Topological Space]] that satisfies the [[knowledge/math/property/topology/Hausdorff Axiom\|Hausdorff Axiom]]: distinct points have disjoint neighborhoods. `[Mun00 §17]`, `[Hat p. 30]`

## Property

> [!theorem] Finite sets are closed
> **Scope**
> - $X$ a Hausdorff space.
>
> ---
> **Property**
> Every finite subset of $X$ is [[knowledge/math/topology/Closed Set\|closed]]: $X$ satisfies the [[knowledge/math/property/topology/T1 Axiom\|T1 Axiom]].
>
> `[Mun00 Thm 17.8]`, `[Hat p. 31]`

> [!theorem] Unique limits — a sequence has at most one limit
> **Scope**
> - $X$ a Hausdorff space.
>
> ---
> **Property**
> A [[knowledge/math/topology/Convergent Sequence\|sequence]] in $X$ converges to at most one point.
>
> `[Mun00 Thm 17.10]`

> [!theorem] Closure under the constructions — orders, products, subspaces
> **Scope**
> - Hausdorff spaces $X$, $Y$; $Z \subseteq X$; a simply ordered set $O$.
>
> ---
> **Property**
> $O$ in the [[knowledge/math/topology/Order Topology\|Order Topology]] is Hausdorff.
> $X \times Y$ in the [[knowledge/math/topology/Product Topology\|Product Topology]] is Hausdorff.
> $Z$ in the [[knowledge/math/topology/Subspace Topology\|Subspace Topology]] is Hausdorff.
>
> `[Mun00 Thm 17.11]`; `[Hat p. 31]` for products and subspaces. Arbitrary products of Hausdorff spaces are Hausdorff in both the box and the product topology `[Mun00 Thm 19.4]` ([[knowledge/math/topology/Product Topology#Box versus product\|Product Topology#Box versus product]]).

> [!proof] Why
> - **Orders.** For $x < y$: if some $z$ lies strictly between, the rays $(-\infty, z)$ and $(z, +\infty)$ separate them; otherwise $(-\infty, y)$ and $(x, +\infty)$ do.
> - **Products.** For $(x_1, y_1) \neq (x_2, y_2)$, say $x_1 \neq x_2$: if $U_1$, $U_2$ separate $x_1$ and $x_2$, then $U_1 \times Y$ and $U_2 \times Y$ separate the pairs.
> - **Subspaces.** If $U_1$, $U_2$ separate two points of $Z$ in $X$, then $U_1 \cap Z$ and $U_2 \cap Z$ separate them in $Z$.

## Example

> [!example] Hausdorff and not
> - $\mathbb R$, $\mathbb R^n$, every metric space, and the [[knowledge/math/topology/example/Topologies on the Real Line\|lower limit and $K$-topologies]].
> - The ordered square $I_o^2$ and $\mathbb R \times \mathbb R$ in the dictionary order, as order topologies.
> - Not: the trivial topology on two or more points; the finite complement topology on an infinite set, where a sequence of distinct points converges to every point ([[knowledge/math/topology/Convergent Sequence#Example\|Convergent Sequence#Example]]).

## Related

### Siblings
- [[knowledge/math/property/topology/T1 Axiom\|T1 Axiom]] — the weaker separation axiom

### Prerequisites
- [[knowledge/math/topology/Topological Space\|Topological Space]], [[knowledge/math/property/topology/Hausdorff Axiom\|Hausdorff Axiom]]
