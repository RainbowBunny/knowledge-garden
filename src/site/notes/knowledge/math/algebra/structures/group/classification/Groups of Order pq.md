---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/classification/groups-of-order-pq/","dg-note-properties":{"aliases":["Groups of Order 2p"]}}
---

Reference:
- `[ConCauApp]` — K. Conrad, _Consequences of Cauchy's theorem_, expository notes, Theorems 3.1, 3.8, Corollary 3.9, Remark 3.11: https://kconrad.math.uconn.edu/blurbs/grouptheory/cauchyapp.pdf
- `[ConSD]` — K. Conrad, _Semidirect products_, expository notes, Lemma 6.2, Theorems 6.1, 6.3: https://kconrad.math.uconn.edu/blurbs/grouptheory/semidirect-product.pdf
- `[ConSylApp]` — K. Conrad, _Consequences of the Sylow theorems_, expository notes, Theorems 4.5, 5.2: https://kconrad.math.uconn.edu/blurbs/grouptheory/sylowapp.pdf
- `[Mil25]` — J. S. Milne, _Group Theory_, course notes v4.01, 2025, Example 1.28 and the table of groups of small order: https://www.jmilne.org/math/CourseNotes/GT.pdf

## Definition

> [!theorem] Groups of Order pq — cyclic unless $q \equiv 1 \bmod p$, and then one nonabelian group more
> ### Scope
> - $p < q$: [[knowledge/math/number theory/Prime\|primes]].
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]] of order $pq$.
>
> ---
> ### Condition
> - $p \neq q$; for $p = q$ see [[Groups of Order p²\|Groups of Order p²]].
>
> ---
> ### Property
> - If $q \not\equiv 1 \bmod p$, then $G \cong C_{pq}$.
> - If $q \equiv 1 \bmod p$, then $G \cong C_{pq}$ or $G \cong C_q \rtimes C_p$, the unique nonabelian group of order $pq$.
>
> `[ConCauApp Thm 3.1, Thm 3.8]` `[ConSD Thm 6.1, Thm 6.3]`

> [!remark] One cyclic group, not two
> $C_p \times C_q \cong C_{pq}$, since $p$ and $q$ are coprime: the element $(1, 1)$ has order $pq$. So the abelian case is a single group.

## Property

> [!proof] Why — a normal Sylow $q$-subgroup and its automorphisms
> $n_q \mid p$ and $n_q \equiv 1 \bmod q$ with $p < q$ force $n_q = 1$, so the Sylow $q$-subgroup $Q \cong C_q$ is normal `[ConSylApp Thm 5.2]` ([[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems\|Sylow Theorems]]). A Sylow $p$-subgroup $P \cong C_p$ meets $Q$ trivially and $|PQ| = pq$, so $G \cong C_q \rtimes_\varphi C_p$ for some $\varphi : C_p \to \mathrm{Aut}(C_q) \cong C_{q-1}$ ([[knowledge/math/algebra/structures/group/extension/Semidirect Product#Internal semidirect product\|Semidirect Product#Internal semidirect product]]). The image of $\varphi$ has order dividing $\gcd(p, q - 1)$. If $p \nmid q - 1$, then $\varphi$ is trivial and $G \cong C_q \times C_p \cong C_{pq}$. If $p \mid q - 1$, the nontrivial $\varphi$ all have the same image, the subgroup of order $p$ of the cyclic group $\mathrm{Aut}(C_q)$, and differ by an automorphism of $C_p$; so they give one group `[ConSD Lemma 6.2, Thm 6.3]`.

> [!remark] As a matrix group `[ConCauApp Thm 3.8]`
> Conrad realizes the nonabelian group as the matrices $\begin{pmatrix} x & y \\ 0 & 1 \end{pmatrix}$ with $x, y \in \mathbb Z/(q)$ and $x^p = 1$.

> [!corollary] Order $2p$ — cyclic or dihedral
> **Scope**
> - $q$: a prime; $G$ of order $2q$.
>
> ---
> **Property**
> $$G \cong C_{2q} \quad \text{or} \quad G \cong D_q.$$
>
> `[ConCauApp Cor 3.9, Rem 3.11]`, for every prime $q$ ([[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]]; $D_2 \cong C_2 \times C_2$).

## Example

> [!example] Small orders `[Mil25 table]`
> - Order 6: $C_6$ and $S_3 \cong D_3$.
> - Order 10: $C_{10}$ and $D_5$.
> - Order 15: only $C_{15}$, since $5 \not\equiv 1 \bmod 3$ `[ConSylApp Thm 4.5]`.
> - Order 21: two groups, since $7 \equiv 1 \bmod 3$.

## Related

### Siblings
- [[Groups of Order p²\|Groups of Order p²]], [[knowledge/math/algebra/structures/group/classification/Groups of Order pqr\|Groups of Order pqr]]

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems\|Sylow Theorems]], [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]], [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|Cyclic Group]]
