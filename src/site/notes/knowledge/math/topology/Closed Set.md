---
{"dg-publish":true,"permalink":"/knowledge/math/topology/closed-set/","dg-note-properties":{"aliases":["Closed","Closed in Y","Closed Subset"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §17: closed sets, Theorems 17.1–17.3.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 4–5, p. 10: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf
- `[Mor]` — S. A. Morris, _Topology Without Tears_, version of October 14, 2007, Definition 1.2.4: https://www.maths.ed.ac.uk/~v1ranick/papers/morris.pdf
- `[Møl]` — J. M. Møller, _General Topology_, lecture notes, University of Copenhagen, Chapter 2: Definition 2.29, Lemma 2.30, Lemma 2.24, Example 2.31: https://www.math.ku.dk/~moller/e03/3gt/notes/gtnotes.pdf

## Intuition

> [!intuition] Why
> Closed sets are the sets that limits cannot escape from. Many statements are more natural for them than for open sets, such as: the set where a continuous function vanishes is closed.

## Definition

> [!definition] Closed Set
> A subset $A$ of a [[knowledge/math/topology/Topological Space\|Topological Space]] $X$ is **closed** iff its complement $X \setminus A$ is open.
>
> `[Mun00 §17]`, `[Hat p. 4]`, `[Mor Def 1.2.4]`, `[Møl Def 2.29]`

> [!definition] Closed in a Subspace
> If $Y$ is a [[knowledge/math/topology/Subspace Topology\|subspace]] of $X$, a set $A$ is **closed in $Y$** iff $A \subseteq Y$ and $A$ is closed in the subspace topology of $Y$, that is, iff $Y \setminus A$ is open in $Y$. `[Mun00 §17]`

> [!warning] Closed is not the opposite of open
> A set can be both, as $\emptyset$ and $X$ always are, or neither, as $[0, 1)$ in $\mathbb R$ is.

## Property

> [!theorem] Closed sets — the dual axioms
> **Scope**
> - $X$ a topological space.
>
> ---
> **Property**
> $\emptyset$ and $X$ are closed.
> Arbitrary intersections of closed sets are closed.
> Finite unions of closed sets are closed.
>
> `[Mun00 Thm 17.1]`, `[Hat p. 5]`, `[Møl Lemma 2.30]`, by De Morgan's laws ([[knowledge/math/set theory/Algebra of Set\|Algebra of Set]]) applied to the axioms of a topology. `[Møl Lemma 2.30]` adds the converse: any family of subsets with these three properties is the family of closed sets of exactly one topology.

> [!theorem] Closed sets of a subspace — intersections with closed sets
> **Scope**
> - $Y$ a subspace of $X$; $A \subseteq Y$.
>
> ---
> **Property**
> $A$ is closed in $Y$ $\iff$ $A = C \cap Y$ for some $C$ closed in $X$.
>
> `[Mun00 Thm 17.2]`. If $Y \setminus A = Y \cap U$ with $U$ open in $X$, take $C = X \setminus U$; conversely $Y \setminus (C \cap Y) = Y \cap (X \setminus C)$.

> [!theorem] Closed subspaces — closed in Y is closed in X
> **Scope**
> - $Y$ closed in $X$; $A$ closed in $Y$.
>
> ---
> **Property**
> $A$ is closed in $X$.
>
> `[Mun00 Thm 17.3]`; `[Hat p. 10]` and `[Møl Lemma 2.24(2)]` state the equivalence. $A = C \cap Y$ is an intersection of two closed sets of $X$. The open version is [[knowledge/math/topology/Subspace Topology#Property\|Lemma 16.2]].

## Example

> [!example] Closed sets of familiar spaces
> - In $\mathbb R$: $[a, b]$ is closed `[Møl Ex 2.31(1)]`, and so are $[a, +\infty)$ and every finite set; $(a, b)$ and $[a, b)$ are not.
> - In the discrete topology every set is closed; in the trivial topology only $\emptyset$ and $X$ are.
> - In the finite complement topology the closed sets are $X$ and the finite sets.
> - In the subspace $Y = [0, 1] \cup (2, 3)$ of $\mathbb R$, both pieces are open and closed in $Y$; in $\mathbb R$, $[0, 1]$ is only closed and $(2, 3)$ only open.

## Related

### Siblings
- [[knowledge/math/topology/Closure and Interior\|Closure and Interior]] — the smallest closed set containing a set

### Prerequisites
- [[knowledge/math/topology/Topological Space\|Topological Space]], [[knowledge/math/topology/Subspace Topology\|Subspace Topology]]
