---
{"dg-publish":true,"permalink":"/knowledge/math/topology/limit-point/","dg-note-properties":{"aliases":["Accumulation Point","Cluster Point","Derived Set"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §17: limit points, Theorem 17.6, Corollary 17.7, Theorem 17.9.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 5–6: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf

## Intuition

> [!intuition] Why
> Limit points are the points a set accumulates at. They let one recognise closed sets without computing complements, and describe approaching a point in spaces without a metric.

## Definition

> [!definition] Limit Point
> Let $A$ be a subset of a [[knowledge/math/topology/Topological Space\|Topological Space]] $X$ and $x \in X$. Then $x$ is a **limit point** of $A$ iff every [[knowledge/math/topology/Closure and Interior\|neighborhood]] of $x$ intersects $A$ in some point other than $x$ itself. Equivalently, $x \in \overline{A \setminus \{x\}}$. The set $A'$ of all limit points of $A$ is its **derived set**.
>
> `[Mun00 §17]`

> [!warning] Two meanings of "limit point"
> `[Hat p. 5]` calls $x$ a limit point of $A$ when every open set containing $x$ meets $A$ — possibly only at $x$ — so for Hatcher the closure **is** the set of limit points. The meaning above, which excludes $x$ itself, is Hatcher's "more restricted meaning" `[Hat p. 6]`, also called a point of accumulation or a cluster point.

## Property

> [!theorem] Closure — the set plus its limit points
> **Scope**
> - $A \subseteq X$, $A'$ its set of limit points.
>
> ---
> **Property**
> $$\overline A = A \cup A'.$$
>
> `[Mun00 Thm 17.6]`. If $x \in \overline A \setminus A$, every neighborhood of $x$ meets $A$, necessarily at a point other than $x$ ([[knowledge/math/topology/Closure and Interior#Property\|Closure and Interior#Property]]).

> [!corollary] Closed — contains its limit points
> **Scope**
> - $A \subseteq X$.
>
> ---
> **Property**
> $A$ is [[knowledge/math/topology/Closed Set\|closed]] $\iff$ $A' \subseteq A$.
>
> `[Mun00 Cor 17.7]`

> [!theorem] Limit points in a T1 space — infinitely many nearby points
> **Scope**
> - $X$ satisfying the [[knowledge/math/property/topology/T1 Axiom\|T1 Axiom]]; $A \subseteq X$; $x \in X$.
>
> ---
> **Property**
> $x$ is a limit point of $A$ $\iff$ every neighborhood of $x$ contains infinitely many points of $A$.
>
> `[Mun00 Thm 17.9]`. ⇐ is clear. ⇒: if $U \ni x$ met $A \setminus \{x\}$ only in the finite set $F$, then $U \setminus F$ would be a neighborhood of $x$, open because $F$ is closed, missing $A \setminus \{x\}$.

## Example

> [!example] Limit points in $\mathbb R$
> - $A = \{1/n : n \in \mathbb Z_{>0}\}$: $A' = \{0\}$; no point of $A$ is a limit point of $A$.
> - $A = (0, 1)$: $A' = [0, 1]$.
> - $A = \mathbb Z$: $A' = \emptyset$, so $\mathbb Z$ is closed.

> [!example] Without T1 the count fails
> In $X = \{a, b\}$ with the trivial topology, $a$ is a limit point of $A = \{b\}$, although its only neighborhood $X$ contains just one point of $A$.

## Related

### Siblings
- [[knowledge/math/topology/Closure and Interior\|Closure and Interior]], [[knowledge/math/topology/Convergent Sequence\|Convergent Sequence]] — limits of sequences are limit points in metric spaces, not in general

### Prerequisites
- [[knowledge/math/topology/Topological Space\|Topological Space]], [[knowledge/math/topology/Closed Set\|Closed Set]]
