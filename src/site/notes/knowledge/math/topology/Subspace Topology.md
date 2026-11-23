---
{"dg-publish":true,"permalink":"/knowledge/math/topology/subspace-topology/","dg-note-properties":{"aliases":["Subspace","Relative Topology","Open in Y"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §16: the subspace topology, Lemmas 16.1, 16.2, Theorems 16.3, 16.4.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 9–10: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf
- `[Møl]` — J. M. Møller, _General Topology_, lecture notes, University of Copenhagen, Chapter 2: Definition 2.22, Lemmas 2.23, 2.24, Theorem 2.25, Lemma 2.27, Example 2.28(5): https://www.math.ku.dk/~moller/e03/3gt/notes/gtnotes.pdf

## Intuition

> [!intuition] Why
> Every subset of a space should be a space in its own right, like $[0, 1]$ inside ℝ or a circle inside the plane. The subspace topology gives it the nearness it inherits from the ambient space.

## Definition

> [!definition] Subspace Topology
> Let $(X, \mathcal T)$ be a [[knowledge/math/topology/Topological Space\|Topological Space]] and $Y \subseteq X$. The **subspace topology** on $Y$ is
> $$\mathcal T_Y = \{Y \cap U : U \in \mathcal T\}.$$
> With it, $Y$ is a **subspace** of $X$.
>
> `[Mun00 §16]`, `[Hat p. 9]`, `[Møl Def 2.22]`. It is a topology because intersecting with $Y$ preserves unions and finite intersections.

> [!remark] Open in $Y$ versus open in $X$
> $U \subseteq Y$ is **open in $Y$** iff $U \in \mathcal T_Y$, and **open in $X$** iff $U \in \mathcal T$ `[Mun00 §16]`. A set open in $Y$ need not be open in $X$ `[Hat p. 10]`: $[0, 1/2) = [0, 1] \cap (-1, 1/2)$ is open in $[0, 1]$ but not in $\mathbb R$.

## Property

> [!lemma] Basis of a subspace — intersect the basis with $Y$
> **Scope**
> - $\mathcal B$ a [[knowledge/math/topology/Basis for a Topology\|basis]] for $\mathcal T$; $Y \subseteq X$.
>
> ---
> **Property**
> $\mathcal B_Y = \{B \cap Y : B \in \mathcal B\}$ is a basis for $\mathcal T_Y$.
>
> `[Mun00 Lemma 16.1]`, `[Hat p. 9]`; `[Møl Lemma 2.23]` adds the same for subbases.

> [!lemma] Open subspaces — open in $Y$ is open in $X$
> **Scope**
> - $Y$ open in $X$; $U \subseteq Y$.
>
> ---
> **Property**
> $U$ open in $Y$ $\Rightarrow$ $U$ open in $X$.
>
> `[Mun00 Lemma 16.2]`; `[Hat p. 10]` and `[Møl Lemma 2.24(2)]` state the equivalence. If $U = Y \cap V$ with $V$ open in $X$, then $U$ is an intersection of two open sets of $X$.

> [!remark] Compatibility with products and orders
> - Taking subspaces commutes with taking products: [[knowledge/math/topology/Product Topology#Property\|Product Topology#Property]], `[Mun00 Thm 16.3]`.
> - On a subset of an ordered set, the order topology is coarser than the subspace topology, and equal to it on convex subsets: [[knowledge/math/topology/Order Topology#Subspaces and convex sets\|Order Topology#Subspaces and convex sets]], `[Mun00 Thm 16.4]`.

## Example

> [!example] Subspaces of $\mathbb R$
> - $[0, 1]$: by Lemma 16.1 the sets $(a, b) \cap [0, 1]$ form a basis, that is, the intervals $(a, b)$, $[0, b)$ and $(a, 1]$ inside $[0, 1]$, and $[0, 1]$ itself `[Mun00 §16]`.
> - $\mathbb Z$: the discrete topology, since $\{n\} = \mathbb Z \cap (n - 1/2, n + 1/2)$.
> - $\mathbb Q$: the subspace topology equals the order topology of $\mathbb Q$ `[Møl Ex 2.28(5)]`.

## Related

### Siblings
- [[knowledge/math/topology/Product Topology\|Product Topology]], [[knowledge/math/topology/Order Topology\|Order Topology]] — the other constructions of §§14–16

### Prerequisites
- [[knowledge/math/topology/Topological Space\|Topological Space]], [[knowledge/math/topology/Basis for a Topology\|Basis for a Topology]]
