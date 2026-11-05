---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/classification/groups-of-order-p-to-the-fourth/","dg-note-properties":{"aliases":["Groups of Order p⁴"]}}
---

Reference:
- `[AGW16]` — J. D. Adler, M. Garlow, E. R. Wheland, _Groups of order p⁴ made less difficult_, 2006, minor changes 2016, Main Theorem, Table 2: https://arxiv.org/pdf/1611.00461
- `[Con16]` — K. Conrad, _Groups of order 16_, expository notes, Table 1: https://kconrad.math.uconn.edu/blurbs/grouptheory/group16.pdf
- `[Höl93]` — O. Hölder, _Die Gruppen der Ordnungen p³, pq², pqr, p⁴_, Math. Ann. 43 (1893), 301–412 — as cited by `[AGW16]`; not read.

## Definition

> [!theorem] Groups of Order p⁴ — fifteen groups for odd $p$, fourteen for $p = 2$
> ### Scope
> - $p$: a [[knowledge/math/number theory/Prime\|Prime]].
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]] of order $p^4$.
>
> ---
> ### Condition
> - The count of nonabelian groups depends on whether $p = 2$.
>
> ---
> ### Property
> - If $G$ is abelian, it is one of five groups:
> $$C_{p^4}, \quad C_{p^3} \times C_p, \quad C_{p^2} \times C_{p^2}, \quad C_{p^2} \times C_p \times C_p, \quad C_p \times C_p \times C_p \times C_p.$$
> - If $p$ is odd, there are exactly 10 nonabelian groups, 15 groups in all `[AGW16 Main Theorem]`.
> - If $p = 2$, there are 9 nonabelian groups, 14 in all `[Con16 Table 1]` — [[knowledge/math/algebra/structures/group/classification/Groups of Order 16\|Groups of Order 16]].

> [!remark] The abelian ones
> The five abelian groups correspond to the partitions $4$, $3 + 1$, $2 + 2$, $2 + 1 + 1$, $1 + 1 + 1 + 1$ of the exponent; `[AGW16]` and `[Con16]` list five abelian groups for odd $p$ and for $p = 2$.

## Property

> [!remark] How `[AGW16]` classifies the nonabelian ones
> Each nonabelian group of order $p^4$ is shown to realize exactly one of ten [[knowledge/math/algebra/structures/group/extension/Cyclic Extension\|extension types]] $(\tau, v)$, listed in their Table 2, with $\tau$ an automorphism of an abelian normal subgroup of order $p^3$ written as a matrix. Their Main Theorem is valid for odd $p$ only; for $p = 2$ they defer to M. Wild's classification of the 14 groups of order 16. The original classification is Hölder's `[Höl93]`.

## Related

### Siblings
- [[Groups of Order p³\|Groups of Order p³]], [[knowledge/math/algebra/structures/group/classification/Groups of Order 16\|Groups of Order 16]]

### Prerequisites
- [[knowledge/math/algebra/structures/group/extension/Cyclic Extension\|Cyclic Extension]], [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]]
