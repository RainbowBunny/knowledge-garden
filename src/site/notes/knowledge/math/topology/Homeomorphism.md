---
{"dg-publish":true,"permalink":"/knowledge/math/topology/homeomorphism/","dg-note-properties":{"aliases":["Homeomorphic","Topological Embedding","Topological Imbedding","Imbedding","Embedding (Topology)"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §18: homeomorphisms, topological imbeddings.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, p. 11 (homeomorphism), p. 13, p. 32: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf

## Intuition

> [!intuition] Why
> Two spaces that differ only in the names of their points should count as the same space. A homeomorphism is a bijection that carries open sets to open sets in both directions, so every topological property, such as being Hausdorff, compact or connected, is shared by homeomorphic spaces. Proving two spaces are not homeomorphic means finding such a property that one has and the other lacks.

## Definition

> [!definition] Homeomorphism
> Extends:: [[knowledge/math/property/map/Continuity\|Continuity]]
>
> ---
> Let $X$, $Y$ be [[knowledge/math/topology/Topological Space\|topological spaces]]. A [[knowledge/math/property/map/Bijection\|Bijection]] $f : X \to Y$ is a **homeomorphism** iff $f$ and $f^{-1} : Y \to X$ are both [[knowledge/math/property/map/Continuity\|continuous]]. Then $X$ and $Y$ are **homeomorphic**.
>
> `[Mun00 §18]`, `[Hat p. 11]`. Equivalently, $f$ is a bijection such that $f(U)$ is open iff $U$ is open.

> [!definition] Topological Imbedding
> An injective continuous map $f : X \to Y$ is a **topological imbedding** (embedding) of $X$ in $Y$ iff the map $f' : X \to f(X)$ obtained by restricting the range is a homeomorphism, where $f(X)$ carries the [[knowledge/math/topology/Subspace Topology\|subspace topology]]. `[Mun00 §18]`

## Property

> [!proposition] Homeomorphic — an equivalence
> **Scope**
> - Topological spaces $X$, $Y$, $Z$.
>
> ---
> **Property**
> $X$ is homeomorphic to $X$.
> If $X$ is homeomorphic to $Y$, then $Y$ is homeomorphic to $X$.
> If $X$ is homeomorphic to $Y$ and $Y$ to $Z$, then $X$ is homeomorphic to $Z$.
>
> Identities, inverses and composites of homeomorphisms are homeomorphisms ([[knowledge/math/property/map/Continuity#Property\|Continuity#Property]]).

## Example

> [!example] Homeomorphic spaces
> - Any open interval $(a, b)$ and $\mathbb R$: $x \mapsto x / (1 - x^2)$ is a homeomorphism $(-1, 1) \to \mathbb R$, and affine maps move $(a, b)$ to $(-1, 1)$ `[Mun00 §18]`.
> - $x \mapsto (x, y_0)$ is a homeomorphism of $X$ onto the slice $X \times \{y_0\}$ of a product, so it is an imbedding of $X$ in $X \times Y$ `[Hat p. 13]`.

> [!example] A continuous bijection that is not a homeomorphism
> - The identity $\mathbb R_\ell \to \mathbb R$ ([[knowledge/math/topology/example/Topologies on the Real Line\|Topologies on the Real Line]]): continuous, since $\mathbb R_\ell$ is finer, but its inverse is not continuous. In general the identity from a finer to a strictly coarser topology is such a map `[Hat p. 32]`.
> - $f : [0, 1) \to S^1$, $f(t) = (\cos 2\pi t, \sin 2\pi t)$, onto the unit circle: continuous and bijective, but $f([0, 1/4))$ is not open in $S^1$, since points of the circle near $f(0)$ come from $t$ near $1$ `[Mun00 §18]`.

## Related

### Siblings
- [[knowledge/math/set theory/order/Order Isomorphism\|Order Isomorphism]] — the same idea for orders
- [[knowledge/math/algebra/category/Morphism\|Morphism]] — a homeomorphism is an isomorphism in the category of topological spaces and continuous maps

### Prerequisites
- [[knowledge/math/property/map/Continuity\|Continuity]], [[knowledge/math/property/map/Bijection\|Bijection]], [[knowledge/math/topology/Subspace Topology\|Subspace Topology]]
