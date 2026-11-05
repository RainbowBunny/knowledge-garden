---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/classification/groups-of-order-30/","dg-note-properties":{}}
---

Reference:
- `[ConSylApp]` — K. Conrad, _Consequences of the Sylow theorems_, expository notes, Lemma 5.3, Theorem 5.9, Corollary 5.10: https://kconrad.math.uconn.edu/blurbs/grouptheory/sylowapp.pdf
- `[ConDih]` — K. Conrad, _Dihedral groups_, expository notes, §1: https://kconrad.math.uconn.edu/blurbs/grouptheory/dihedral.pdf

## Definition

> [!theorem] Groups of Order 30 — four groups: $C_{30}$, $D_{15}$, $C_3 \times D_5$, $C_5 \times D_3$
> ### Scope
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]] of order $30 = 2 \cdot 3 \cdot 5$.
>
> ---
> ### Condition
> - None.
>
> ---
> ### Property
> - $G$ has normal Sylow 3- and Sylow 5-subgroups `[ConSylApp Thm 5.9]`.
> - $G$ is isomorphic to exactly one of
> $$C_{30}, \qquad D_{15}, \qquad C_3 \times D_5, \qquad C_5 \times D_3$$
> `[ConSylApp Cor 5.10]`, which writes $S_3$ for $D_3$.

## Property

> [!proof] Why — a normal cyclic subgroup of index 2
> 1. **One of $P_3$, $P_5$ is normal.** By the [[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems\|Sylow Theorems]], $n_3 \in \{1, 10\}$ and $n_5 \in \{1, 6\}$. If $n_3 = 10$ and $n_5 = 6$, there would be $10 \cdot 2 = 20$ elements of order 3 and $6 \cdot 4 = 24$ of order 5 ([[knowledge/math/algebra/structures/group/subgroup/Sylow Subgroup#Property\|Sylow Subgroup#Property]]), and $1 + 20 + 24 = 45 > 30$.
> 2. **$H = P_3 P_5$ is a cyclic normal subgroup of order 15.** One of $P_3$, $P_5$ is normal, so $H$ is a subgroup, of order 15 since $P_3 \cap P_5 = \{e\}$ ([[knowledge/math/algebra/structures/group/subgroup/Normalizer#Products of subgroups\|Normalizer#Products of subgroups]]). It has index 2, so it is normal, and it is cyclic ([[knowledge/math/algebra/structures/group/classification/Groups of Order pq\|Groups of Order pq]]: $5 \not\equiv 1 \bmod 3$). Its Sylow subgroups $P_3$, $P_5$ are characteristic in $H$, hence normal in $G$.
> 3. **$G \cong C_{15} \rtimes C_2$.** A Sylow 2-subgroup $\langle y \rangle \cong C_2$ is a complement to $H = \langle x \rangle$, and $yxy^{-1} = x^k$ with $k^2 \equiv 1 \bmod 15$ ([[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]]).
> 4. **Four actions.** $k \equiv \pm 1 \bmod 3$ and $k \equiv \pm 1 \bmod 5$, so $k \in \{1, 4, 11, 14\}$ by the Chinese remainder theorem:
>     - $k = 1$: $C_{15} \times C_2 \cong C_{30}$;
>     - $k = 14 \equiv -1$: $y$ inverts $x$, the [[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]] $D_{15}$;
>     - $k = 4$: $y$ fixes $x^5$ (order 3) and inverts $x^3$ (order 5): $C_3 \times D_5$;
>     - $k = 11$: $y$ inverts $x^5$ and fixes $x^3$: $C_5 \times D_3$.

> [!proposition] Telling them apart — the number of elements of order 2
> **Scope**
> - The four groups above.
>
> ---
> **Property**
> 
> | group | elements of order 2 |
> | --- | --- |
> | $C_{30}$ | 1 |
> | $D_{15}$ | 15 |
> | $C_3 \times D_5$ | 5 |
> | $C_5 \times D_3$ | 3 |
>
> In $C_3 \times D_5$ an element $(c, d)$ has order 2 iff $c = e$ and $d$ has order 2, and $D_5$ has 5 elements of order 2 `[ConDih §1]`; similarly for $C_5 \times D_3$. The counts differ, so the four groups are pairwise non-isomorphic.

## Example

> [!example] Not covered by Burnside's theorem
> 30 has three prime factors, so [[knowledge/math/algebra/structures/group/special group/Burnside's Solvability Theorem\|Burnside's Solvability Theorem]] does not apply; the proof above shows directly that every group of order 30 is solvable: $\{e\} \subset C_{15} \subset G$ has abelian factors ([[knowledge/math/algebra/structures/group/special group/Solvable Group\|Solvable Group]]).

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/classification/Groups of Order pqr\|Groups of Order pqr]] — the general case $p < q < r$; here the Sylow 3-subgroup is normal too
- [[knowledge/math/algebra/structures/group/classification/Groups of Order pq\|Groups of Order pq]] — order 15 inside

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems\|Sylow Theorems]], [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]], [[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]]
