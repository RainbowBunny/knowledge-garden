---
{"dg-publish":true,"permalink":"/knowledge/math/topology/closure-and-interior/","dg-note-properties":{"aliases":["Closure (Topology)","Topological Closure","Interior","Neighborhood","Neighbourhood","Intersects"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §17: interior, closure, neighborhoods, Theorems 17.4, 17.5.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 5–6 (interior, closure, Proposition 1.1), p. 8, p. 10: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf

## Intuition

> [!intuition] Why
> The closure adds every point that is arbitrarily close to the set; the interior keeps only the points with room around them. Together they describe boundaries and density (ℚ is dense in ℝ) in any topological space.

## Definition

> [!definition] Parameters
> - $X$: a [[knowledge/math/topology/Topological Space\|Topological Space]]; $A \subseteq X$.

> [!definition] Interior and Closure
> - The **interior** $\mathrm{Int}\, A$ is the union of all open sets contained in $A$.
> - The **closure** $\overline A$ is the intersection of all [[knowledge/math/topology/Closed Set\|closed sets]] containing $A$.
>
> `[Mun00 §17]`. So $\mathrm{Int}\, A$ is the largest open set inside $A$, $\overline A$ is the smallest closed set containing $A$, and $\mathrm{Int}\, A \subseteq A \subseteq \overline A$.

> [!definition] Intersects, Neighborhood
> - $A$ **intersects** $B$ iff $A \cap B \neq \emptyset$.
> - A **neighborhood** of $x$ is an open set containing $x$.
>
> `[Mun00 §17]`. Some authors let a neighborhood be any set containing an open set around $x$; Munkres does not.

## Property

> [!theorem] Closure by neighborhoods — every neighborhood meets A
> **Scope**
> - $A \subseteq X$; $x \in X$.
>
> ---
> **Property**
> $x \in \overline A$ $\iff$ every neighborhood of $x$ intersects $A$.
> If the topology is given by a [[knowledge/math/topology/Basis for a Topology\|basis]]: $x \in \overline A$ $\iff$ every basis element containing $x$ intersects $A$.
>
> `[Mun00 Thm 17.5]`; `[Hat p. 5]` takes the first line as the definition of the closure. Contrapositive: $x \notin \overline A$ iff some open $U \ni x$ misses $A$, iff $x$ lies in the open set $X \setminus \overline A$.

> [!theorem] Closure in a subspace — intersect with Y
> **Scope**
> - $Y$ a [[knowledge/math/topology/Subspace Topology\|subspace]] of $X$; $A \subseteq Y$; $\overline A$ the closure in $X$.
>
> ---
> **Property**
> The closure of $A$ in $Y$ is $\overline A \cap Y$.
>
> `[Mun00 Thm 17.4]`, `[Hat p. 10]`. The closed sets of $Y$ are the sets $C \cap Y$ with $C$ closed in $X$ ([[knowledge/math/topology/Closed Set#Property\|Closed Set#Property]]).

> [!proposition] Basic facts
> **Scope**
> - $A, B \subseteq X$.
>
> ---
> **Property**
> $\mathrm{Int}\, A$ is open and $\overline A$ is closed.
> $A$ is open iff $A = \mathrm{Int}\, A$; $A$ is closed iff $A = \overline A$.
> $X \setminus \overline A = \mathrm{Int}\,(X \setminus A)$.
>
> `[Hat Prop 1.1]` for the first line; the others follow from the definitions.

## Example

> [!example] Closures in $\mathbb R$
> - $\overline{(0, 1]} = [0, 1]$ and $\mathrm{Int}\, (0, 1] = (0, 1)$.
> - $\overline{\{1/n : n \in \mathbb Z_{>0}\}} = \{0\} \cup \{1/n\}$.
> - $\overline{\mathbb Q} = \mathbb R$ and $\mathrm{Int}\, \mathbb Q = \emptyset$.
> - In the subspace $Y = (0, 1]$, the closure of $(0, 1/2)$ is $(0, 1/2]$, not $[0, 1/2]$, by Theorem 17.4.

## Related

### Siblings
- [[knowledge/math/topology/Limit Point\|Limit Point]] — $\overline A = A \cup A'$
- [[knowledge/math/topology/Closed Set\|Closed Set]]

### Prerequisites
- [[knowledge/math/topology/Topological Space\|Topological Space]], [[knowledge/math/topology/Basis for a Topology\|Basis for a Topology]]
