---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/classification/groups-of-order-pqr/","dg-note-properties":{}}
---

Reference:
- `[Dart13]` — Dartmouth College, Math 101 (Fall 2013), Homework 6 solutions, Problem 4 and the comment after it: https://gauss.dartmouth.edu/~m101f13/hw6-solns.pdf
- `[ConSylApp]` — K. Conrad, _Consequences of the Sylow theorems_, expository notes, Theorem 5.11, Theorem 5.12, Corollary 5.13: https://kconrad.math.uconn.edu/blurbs/grouptheory/sylowapp.pdf
- `[ConSZ]` — K. Conrad, _The Schur–Zassenhaus theorem_, expository notes, Theorem 1: https://kconrad.math.uconn.edu/blurbs/grouptheory/schurzass.pdf
- `[Höl93]` — O. Hölder, _Die Gruppen der Ordnungen p³, pq², pqr, p⁴_, Math. Ann. 43 (1893), 301–412 — the full classification, as cited by `[AGW16]` (Adler, Garlow, Wheland, arXiv:1611.00461); not read.

## Definition

> [!theorem] Groups of Order pqr — the Sylow subgroup for the largest prime is normal
> ### Scope
> - $p < q < r$: [[knowledge/math/number theory/Prime\|primes]].
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]] of order $pqr$.
> - $R$: a [[knowledge/math/algebra/structures/group/subgroup/Sylow Subgroup\|Sylow $r$-subgroup]] of $G$, of order $r$.
>
> ---
> ### Condition
> - Three distinct primes.
>
> ---
> ### Property
> $$R \trianglelefteq G.$$
>
> `[Dart13 Problem 4]`. The problem asks only that one of the Sylow subgroups be normal; the comment after it, credited to J. Troyka, proves that $R$ always is.

## Property

> [!proof] Why — count elements, then pass through $QR$
> Suppose $n_r > 1$. Since $n_r \mid pq$ and $n_r \equiv 1 \bmod r$ with $p, q < r$, $n_r = pq$, which gives $pq(r - 1)$ elements of order $r$ ([[knowledge/math/algebra/structures/group/subgroup/Sylow Subgroup#Property\|Sylow Subgroup#Property]]). If also $n_q > 1$, then $n_q \mid pr$, $n_q \equiv 1 \bmod q$ and $p < q$ force $n_q \geq r$, which gives at least $r(q - 1)$ elements of order $q$. Then
> $$pq(r - 1) + r(q - 1) = pqr + r(q - 1) - pq > pqr,$$
> since $r(q - 1) \geq (q + 1)(q - 1) > q(q - 1) \geq pq$. So $n_q = 1$ and the Sylow $q$-subgroup $Q$ is normal. In $G/Q$, of order $pr$, the Sylow $r$-subgroup is normal ([[knowledge/math/algebra/structures/group/classification/Groups of Order pq\|Groups of Order pq]]); its preimage $QR$ is a normal subgroup of order $qr$. In $QR$, $R$ is the unique Sylow $r$-subgroup, hence preserved by every automorphism of $QR$, so normal in $G$: against $n_r > 1$.
>
> `[Dart13]`

> [!corollary] A semidirect product with a group of order $pq$
> **Scope**
> - $G$, $R$: as above.
>
> ---
> **Property**
> $G$ has a subgroup $H$ of order $pq$, and
> $$G \cong C_r \rtimes H,$$
> with $H$ one of the [[knowledge/math/algebra/structures/group/classification/Groups of Order pq\|Groups of Order pq]].
>
> $\gcd(r, pq) = 1$, so the [[knowledge/math/algebra/structures/group/extension/Schur-Zassenhaus Theorem\|Schur-Zassenhaus Theorem]] gives the complement `[ConSZ Thm 1]`. What is left is to list the actions $H \to \mathrm{Aut}(C_r) \cong C_{r-1}$ up to isomorphism; Hölder did this in 1893 `[Höl93]`.

> [!corollary] Abelian case — an abelian group of order $pqr$ is cyclic
> Each Sylow subgroup is normal and of prime order, so $G \cong C_p \times C_q \times C_r \cong C_{pqr}$ ([[knowledge/math/algebra/structures/group/extension/Semidirect Product#Internal semidirect product\|Semidirect Product#Internal semidirect product]]).

## Example

> [!example] Order 30 and 105
> - $30 = 2 \cdot 3 \cdot 5$: four groups — [[knowledge/math/algebra/structures/group/classification/Groups of Order 30\|Groups of Order 30]].
> - $105 = 3 \cdot 5 \cdot 7$: the Sylow 5- and 7-subgroups are normal, and there are two groups `[ConSylApp Thm 5.11, Thm 5.12, Cor 5.13]`.

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/classification/Groups of Order pq\|Groups of Order pq]], [[knowledge/math/algebra/structures/group/classification/Groups of Order 30\|Groups of Order 30]]

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems\|Sylow Theorems]], [[knowledge/math/algebra/structures/group/extension/Schur-Zassenhaus Theorem\|Schur-Zassenhaus Theorem]], [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]]
