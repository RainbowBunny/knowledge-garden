---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/classification/groups-of-order-p-cubed/","dg-note-properties":{"aliases":["Groups of Order p³","Groups of Order 8","Heisenberg Group mod p"]}}
---

Reference:
- `[ConP3]` — K. Conrad, _Groups of order p³_, expository notes, §1, Theorem 2.1, Lemma 3.2, Theorems 3.4, 4.1: https://kconrad.math.uconn.edu/blurbs/grouptheory/groupsp3.pdf

## Definition

> [!theorem] Groups of Order p³ — three abelian groups and two nonabelian ones, for every prime $p$
> ### Scope
> - $p$: a [[knowledge/math/number theory/Prime\|Prime]].
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]] of order $p^3$.
>
> ---
> ### Condition
> - The two nonabelian groups are different for $p = 2$ and for odd $p$.
>
> ---
> ### Property
> - If $G$ is abelian: $G \cong C_{p^3}$, $C_{p^2} \times C_p$ or $C_p \times C_p \times C_p$ `[ConP3 §1]`.
> - If $p = 2$ and $G$ is nonabelian: $G \cong D_4$ or $Q_8$ `[ConP3 Thm 2.1]`.
> - If $p$ is odd and $G$ is nonabelian: $G \cong \mathrm{Heis}(\mathbb Z/(p))$ or $G \cong G_p$ `[ConP3 Thm 3.4]`.

> [!example] The two nonabelian groups for odd $p$ `[ConP3 §3]`
> - $\mathrm{Heis}(\mathbb Z/(p))$: the upper unitriangular matrices $\begin{pmatrix} 1 & a & b \\ 0 & 1 & c \\ 0 & 0 & 1 \end{pmatrix}$ with $a, b, c \in \mathbb Z/(p)$. Every nonidentity element has order $p$.
> - $G_p$: the matrices $\begin{pmatrix} m & b \\ 0 & 1 \end{pmatrix}$ with $b \in \mathbb Z/(p^2)$ and $m \in (\mathbb Z/(p^2))^\times$, $m \equiv 1 \bmod p$. It has elements of order $p^2$; the source notes it has no standard name.

## Property

> [!lemma] Nonabelian structure — center of order $p$, quotient $C_p \times C_p$
> **Scope**
> - $G$: a nonabelian group of order $p^3$, with center $Z$.
>
> ---
> **Property**
> $$|Z| = p,$$
> $$G/Z \cong C_p \times C_p,$$
> $$[G, G] = Z.$$
>
> `[ConP3 Lemma 3.2]`, for every prime $p$: $G/Z$ cannot be cyclic when $G$ is nonabelian.

> [!remark] Telling the groups apart
> - The abelian ones differ in their largest element order: $p^3$, $p^2$, $p$ `[ConP3 §1]`.
> - $D_4$ has five elements of order 2 and $Q_8$ one ([[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]], [[knowledge/math/algebra/structures/group/example/Generalized Quaternion Group\|Generalized Quaternion Group]]).
> - For odd $p$, $\mathrm{Heis}(\mathbb Z/(p))$ has exponent $p$ and $G_p$ exponent $p^2$. $G_p$ and $C_p \times C_{p^2}$ even have the same subgroup lattice; for $p = 2$ the analogous statement fails `[ConP3 Thm 4.1]`.

## Example

> [!example] Order 8
> $C_8$, $C_4 \times C_2$, $C_2 \times C_2 \times C_2$, $D_4$, $Q_8$: five groups.

## Related

### Siblings
- [[Groups of Order p²\|Groups of Order p²]] — all abelian
- [[Groups of Order p⁴\|Groups of Order p⁴]] — fifteen groups for odd $p$, fourteen for $p = 2$

### Prerequisites
- [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]], [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]], [[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]], [[knowledge/math/algebra/structures/group/example/Generalized Quaternion Group\|Generalized Quaternion Group]]
