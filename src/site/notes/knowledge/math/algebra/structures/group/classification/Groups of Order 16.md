---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/classification/groups-of-order-16/","dg-note-properties":{}}
---

Reference:
- `[Con16]` — K. Conrad, _Groups of order 16_, expository notes, Table 1 and §2 (the invariants): https://kconrad.math.uconn.edu/blurbs/grouptheory/group16.pdf
- `[Wil05]` — M. Wild, _The groups of order sixteen made easy_, Amer. Math. Monthly 112 (2005), no. 1, 20–31 — the proof that the list is complete, as cited by `[Con16]` and `[AGW16]`; not read.
- `[AGW16]` — J. D. Adler, M. Garlow, E. R. Wheland, _Groups of order p⁴ made less difficult_, 2006, minor changes 2016, §1 (extension types): https://arxiv.org/pdf/1611.00461
- `[Mil25]` — J. S. Milne, _Group Theory_, course notes v4.01, 2025, the table of groups of small order: https://www.jmilne.org/math/CourseNotes/GT.pdf

## Definition

> [!theorem] Groups of Order 16 — fourteen groups, five abelian and nine nonabelian
> ### Scope
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]] of order 16.
>
> ---
> ### Condition
> - None.
>
> ---
> ### Property
> $G$ is isomorphic to exactly one of:
> - abelian: $C_{16}$, $C_8 \times C_2$, $C_4 \times C_4$, $C_4 \times C_2 \times C_2$, $C_2^4$;
> - nonabelian: $D_8$, $D_4 \times C_2$, $Q_8 \times C_2$, $Q_8 \rtimes C_2$, $Q_{16}$, $C_8 \rtimes_3 C_2$, $C_8 \rtimes_5 C_2$, $C_4 \rtimes C_4$, $C_2^2 \rtimes C_4$.
>
> `[Con16 Table 1]`, which credits the classification to Hölder and Young (1893) and its completeness proof to `[Wil05]`; `[Mil25]` gives the count $5 + 9 = 14$. Here $D_n$ has order $2n$ ([[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]]), $Q_{16}$ is the [[knowledge/math/algebra/structures/group/example/Generalized Quaternion Group\|Generalized Quaternion Group]], and $C_8 \rtimes_j C_2$ has the generator of $C_2$ acting by $x \mapsto x^j$.

> [!remark] Other names
> $C_8 \rtimes_3 C_2$ is the **semidihedral** group $SD_{16}$, $C_8 \rtimes_5 C_2$ the **modular** group $M_{16}$, and $Q_8 \rtimes C_2$ the **Pauli** group. `[Con16]` uses none of these names. With the $D_{2n}$ convention, $D_8$ is written $D_{16}$.

## Property

### As cyclic extensions of a group of order 8

> [!proposition] Extension types realizing the fourteen groups
> **Scope**
> - $N$: a normal subgroup of order 8 with $G/N \cong C_2$, and $a \in G \setminus N$.
> - $\tau(n) = ana^{-1}$, $v = a^2$: the [[knowledge/math/algebra/structures/group/extension/Cyclic Extension\|extension type]] $(N, 2, \tau, v)$. $N$ is abelian here, so $\tau^2 = \mathrm{id}$ and $\tau(v) = v$.
>
> ---
> **Property**
> With $N = C_8 = \langle x \rangle$:
>
> | $\tau(x)$ | $v$ | group |
> | --- | --- | --- |
> | $x$ | $e$ | $C_8 \times C_2$ |
> | $x$ | $x$ | $C_{16}$ |
> | $x^3$ | $e$ | $C_8 \rtimes_3 C_2$ |
> | $x^5$ | $e$ | $C_8 \rtimes_5 C_2$ |
> | $x^7$ | $e$ | $D_8$ |
> | $x^7$ | $x^4$ | $Q_{16}$ |
>
> With $N = C_4 \times C_2 = \langle x \rangle \times \langle y \rangle$, and the automorphisms $\psi_3 : (x, y) \mapsto (x^{-1}, y)$, $\psi_5 : (x, y) \mapsto (xy, y)$, $\psi_6 : (x, y) \mapsto (x^{-1}, x^2 y)$:
>
> | $\tau$ | $v$ | group |
> | --- | --- | --- |
> | $\mathrm{id}$ | $e$ | $C_4 \times C_2 \times C_2$ |
> | $\mathrm{id}$ | $y$ | $C_4 \times C_4$ |
> | $\psi_3$ | $e$ | $D_4 \times C_2$ |
> | $\psi_3$ | $x^2$ | $Q_8 \times C_2$ |
> | $\psi_5$ | $e$ | $C_2^2 \rtimes C_4$ |
> | $\psi_5$ | $x^2$ | $C_4 \rtimes C_4$ |
> | $\psi_6$ | $e$ | $Q_8 \rtimes C_2$ |
>
> With $N = C_2^3$: $\tau = \mathrm{id}$, $v = e$ gives $C_2^4$.
>
> This is the method of `[Wil05]` as described in `[AGW16]`. `⚠️ CLAUDE – verify:` the tables are mine; I checked each row against the invariants below, but not against `[Wil05]`.

> [!proof] How the rows are identified
> - Read off the presentation: $\langle x, a \mid x^8, a^2 = v, axa^{-1} = \tau(x) \rangle$ for $N = C_8$. For instance $(x^7, x^4)$ is the presentation of $Q_{16}$, and $(x, x)$ makes $a$ of order 16.
> - For $(\psi_5, e)$: $\langle y, a \rangle \cong C_2^2$ is normal, and $\langle x \rangle \cong C_4$ is a complement acting by $a \mapsto ya$.
> - For $(\psi_6, e)$: the center is $\langle xy \rangle \cong C_4$, cyclic, and every element has order at most 4. Among the nonabelian groups of order 16 with cyclic center of order 4, only $C_8 \rtimes_5 C_2$ has elements of order 8, so this is $Q_8 \rtimes C_2$.
> - For $(\psi_5, x^2)$: the center is $\{e, x^2, y, x^2 y\} \cong C_2^2$, there are 3 elements of order 2, and the nontrivial central squares are $x^2$ and $y = (xa)^2$; two central squares separate $C_4 \rtimes C_4$ from $Q_8 \times C_2$ `[Con16 §2]`.

> [!remark] Telling the fourteen apart `[Con16 §2]`
> 1. The number of elements of each order 1, 2, 4, 8, 16 separates most of them.
> 2. Abelian or not separates $C_8 \times C_2$ from $C_8 \rtimes_5 C_2$, which have the same counts and the same subgroup lattice.
> 3. Whether the center is cyclic separates $Q_8 \rtimes C_2$ from $C_2^2 \rtimes C_4$.
> 4. The number of nontrivial central elements that are squares separates $Q_8 \times C_2$ from $C_4 \rtimes C_4$, whose centers are both $C_2^2$.
>
> A nonabelian group of order 16 has a center of order 2 or 4.

## Example

> [!example] Central extensions
> Every nonabelian group of order 16 has a central subgroup of order 2, so it is a central [[knowledge/math/algebra/structures/group/extension/Group Extension\|Group Extension]] of one of the five [[Groups of Order p³\|groups of order 8]] by $C_2$. The cyclic-extension tables above are a more practical way to organize the same groups.

## Related

### Siblings
- [[Groups of Order p⁴\|Groups of Order p⁴]] — the odd-prime analogue, with fifteen groups
- [[Groups of Order p³\|Groups of Order p³]] — the groups of order 8

### Prerequisites
- [[knowledge/math/algebra/structures/group/extension/Cyclic Extension\|Cyclic Extension]], [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]], [[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]], [[knowledge/math/algebra/structures/group/example/Generalized Quaternion Group\|Generalized Quaternion Group]]
