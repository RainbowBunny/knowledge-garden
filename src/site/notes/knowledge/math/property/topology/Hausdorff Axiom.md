---
{"dg-publish":true,"permalink":"/knowledge/math/property/topology/hausdorff-axiom/","dg-note-properties":{"aliases":["T2 Axiom","T2 Separation Axiom","Hausdorff Condition","Hausdorff Separation Axiom"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §17: Hausdorff spaces, Theorem 17.8.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 30–31: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf

## Intuition

> [!intuition] Why
> The axiom that makes limits unique. It is stated on its own so that structures can require it by link, the way groups require associativity.

## Definition

> [!definition] Hausdorff Axiom
> ### Scope
> A [[knowledge/math/topology/Topological Space\|Topological Space]] $X$.
>
> ---
> ### Property
> $X$ satisfies the **Hausdorff axiom** iff any two distinct points have disjoint [[knowledge/math/topology/Closure and Interior\|neighborhoods]]:
> $$\forall x_1 \neq x_2 \in X\; \exists U_1 \ni x_1,\ U_2 \ni x_2 \text{ open}: U_1 \cap U_2 = \emptyset.$$
>
> `[Mun00 §17]`, `[Hat p. 30]`

## Property

> [!proposition] Points are closed — Hausdorff implies T1
> **Scope**
> - $X$ satisfying the Hausdorff axiom.
>
> ---
> **Property**
> Every finite subset of $X$ is closed: $X$ satisfies the [[knowledge/math/property/topology/T1 Axiom\|T1 Axiom]].
>
> `[Mun00 Thm 17.8]`, `[Hat p. 31]`. For $y \neq x$, a neighborhood of $y$ disjoint from a neighborhood of $x$ misses $x$; so $X \setminus \{x\}$ is open.

## Example

> [!example] Where it holds and where it fails
> - Metric spaces: for $x \neq y$ the balls of radius $d(x, y)/2$ are disjoint.
> - Discrete spaces; [[knowledge/math/topology/example/Topologies on the Real Line\|$\mathbb R_\ell$ and $\mathbb R_K$]], since they are finer than the standard topology.
> - Not the trivial topology on two or more points, and not the finite complement topology on an infinite set.

## Related

### Descendants
- [[knowledge/math/topology/Hausdorff Space\|Hausdorff Space]] — a topological space that satisfies this axiom

### Siblings
- [[knowledge/math/property/topology/T1 Axiom\|T1 Axiom]] — the weaker axiom, implied by this one
