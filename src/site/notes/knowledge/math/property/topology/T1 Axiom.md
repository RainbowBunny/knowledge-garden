---
{"dg-publish":true,"permalink":"/knowledge/math/property/topology/t1-axiom/","dg-note-properties":{"aliases":["T1 Separation Axiom","T1 Space","Finite Sets Are Closed"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §17: the $T_1$ axiom, Theorems 17.8, 17.9.

## Intuition

> [!intuition] Why
> The weakest useful separation of points: every point is closed, so removing finitely many points from an open set leaves an open set.

## Definition

> [!definition] T1 Axiom
> ### Scope
> A [[knowledge/math/topology/Topological Space\|Topological Space]] $X$.
>
> ---
> ### Property
> $X$ satisfies the **$T_1$ axiom** iff every finite subset of $X$ is [[knowledge/math/topology/Closed Set\|closed]]:
> $$\forall F \subseteq X: F \text{ finite} \Rightarrow X \setminus F \text{ is open}.$$
>
> `[Mun00 §17]`. Since finite unions of closed sets are closed, it is enough that every one-point set $\{x\}$ is closed.

## Property

> [!proposition] Weaker than Hausdorff
> **Scope**
> - $X$ a topological space.
>
> ---
> **Property**
> [[knowledge/math/property/topology/Hausdorff Axiom\|Hausdorff Axiom]] $\Rightarrow$ $T_1$ axiom.
>
> `[Mun00 Thm 17.8]`. The converse fails: see the example.

> [!proposition] Limit points need infinitely many points
> In a $T_1$ space, $x$ is a [[knowledge/math/topology/Limit Point\|limit point]] of $A$ iff every neighborhood of $x$ contains infinitely many points of $A$ `[Mun00 Thm 17.9]`.

## Example

> [!example] Where it holds and where it fails
> - Every [[knowledge/math/topology/Hausdorff Space\|Hausdorff Space]]: $\mathbb R$, every metric space, every ordered set in the [[knowledge/math/topology/Order Topology\|order topology]].
> - The finite complement topology on an infinite set is $T_1$, by definition of its closed sets, but not Hausdorff: two nonempty open sets always intersect.
> - The trivial topology on a set with two or more points is not $T_1$: $\{x\}$ is not closed.

## Related

### Siblings
- [[knowledge/math/property/topology/Hausdorff Axiom\|Hausdorff Axiom]] — the stronger separation axiom, $T_2$
