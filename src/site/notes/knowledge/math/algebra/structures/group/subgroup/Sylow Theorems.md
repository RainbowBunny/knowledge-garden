---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/subgroup/sylow-theorems/","dg-note-properties":{"aliases":["Sylow's Theorems","First Sylow Theorem","Second Sylow Theorem","Third Sylow Theorem"]}}
---

Reference:
- `[ConSyl]` — K. Conrad, _The Sylow theorems_, expository notes, Theorems 1.7–1.10, equation (2.1), §3: https://kconrad.math.uconn.edu/blurbs/grouptheory/sylowpf.pdf
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_, HTML edition, §15.1: Theorems 15.1.4, 15.1.7, 15.1.8: https://judsonbooks.org/aata-files/aata-html/sylow-section-sylow-theorems.html (result numbers as there).

## Definition

> [!theorem] Sylow Theorems — Sylow $p$-subgroups exist, are all conjugate, and their number is $1 \bmod p$ and divides $m$
> ### Scope
> - $G$: a finite [[knowledge/math/algebra/structures/group/Group\|Group]].
> - $p$: a [[knowledge/math/number theory/Prime\|Prime]], with $|G| = p^k m$ and $p \nmid m$.
> - $n_p$: the number of [[knowledge/math/algebra/structures/group/subgroup/Sylow Subgroup\|Sylow $p$-subgroups]] of $G$.
>
> ---
> ### Condition
> - None: $k = 0$ is allowed, with $\{e\}$ the only Sylow $p$-subgroup.
>
> ---
> ### Property
> - **Existence** — $G$ has a Sylow $p$-subgroup, and every [[knowledge/math/algebra/structures/group/special group/p-Group\|$p$-subgroup]] of $G$ lies in one `[ConSyl Thm 1.7]`.
> - **Conjugacy** — any two Sylow $p$-subgroups are conjugate `[ConSyl Thm 1.8]`.
> - **Counting** — $n_p \mid m$ and $n_p \equiv 1 \bmod p$ `[ConSyl Thm 1.9]`.
> - **Index** — $n_p = [G : N_G(P)]$ for any $P \in \mathrm{Syl}_p(G)$ ([[knowledge/math/algebra/structures/group/subgroup/Normalizer\|Normalizer]]) `[ConSyl Thm 1.10]`.

> [!remark] Judson's statements `[Jud §15.1]`
> - First (Thm 15.1.4): if $p^r$ divides $|G|$, then $G$ contains a subgroup of order $p^r$.
> - Second (Thm 15.1.7): all Sylow $p$-subgroups are conjugate.
> - Third (Thm 15.1.8): $n_p \equiv 1 \bmod p$ and $n_p$ divides $|G|$, weaker than $n_p \mid m$.

## Property

### Subgroups of every $p$-power order

> [!proposition] A chain of $p$-subgroups — subgroups of order $p^i$ for every $p^i$ dividing $|G|$
> **Scope**
> - $G$: a finite group, $p^k$ the largest power of $p$ dividing $|G|$.
>
> ---
> **Property**
> There are subgroups
> $$\{e\} = H_0 \subset H_1 \subset \cdots \subset H_k, \qquad |H_i| = p^i.$$
>
> `[ConSyl §3]`: a finite $p$-group of order $p^k$ contains an increasing chain of subgroups of orders $p^0, \dots, p^k$; applied to a Sylow $p$-subgroup, it gives a subgroup of each order $p^i$ dividing $|G|$. Conrad's proof of existence builds the chain upward: a subgroup $H$ of order $p^i < p^k$ lies in $N_G(H)$, and [[knowledge/math/algebra/structures/group/Cauchy's Theorem\|Cauchy's Theorem]] gives a subgroup of order $p$ in $N_G(H)/H$, whose preimage has order $p^{i+1}$ `[ConSyl §2]`.

### Why the counting holds

> [!proof] $n_p \equiv 1 \bmod p$, by the fixed-point congruence
> Let $P \in \mathrm{Syl}_p(G)$ act by conjugation on $\mathrm{Syl}_p(G)$. A [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]] acting on a finite set has $|X| \equiv |\mathrm{Fix}(X)| \bmod p$ `[ConSyl (2.1)]` ([[knowledge/math/algebra/structures/action/Group Action#Property\|Group Action#Property]]). If $Q$ is fixed, then $P \leq N_G(Q)$, so $PQ$ is a $p$-subgroup ([[knowledge/math/algebra/structures/group/subgroup/Normalizer#Products of subgroups\|Normalizer#Products of subgroups]]) containing both; maximality gives $P = PQ = Q$. So $P$ is the only fixed point, and $n_p \equiv 1 \bmod p$. For $n_p \mid m$: $G$ acts transitively on $\mathrm{Syl}_p(G)$ by conjugation, so $n_p = [G : N_G(P)]$, which divides $[G : P] = m$ since $P \leq N_G(P)$.

## Example

> [!example] Forcing a normal Sylow subgroup
> - $|G| = pq$, $p < q$: $n_q \mid p$ and $n_q \equiv 1 \bmod q$ force $n_q = 1$ — [[knowledge/math/algebra/structures/group/classification/Groups of Order pq\|Groups of Order pq]].
> - $|G| = 30$: $n_3 \in \{1, 10\}$, $n_5 \in \{1, 6\}$, and counting elements excludes $n_3 = 10$ with $n_5 = 6$ — [[knowledge/math/algebra/structures/group/classification/Groups of Order 30\|Groups of Order 30]].
> - $|G| = pqr$, $p < q < r$: the Sylow $r$-subgroup is normal — [[knowledge/math/algebra/structures/group/classification/Groups of Order pqr\|Groups of Order pqr]].

## Related

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Sylow Subgroup\|Sylow Subgroup]], [[knowledge/math/algebra/structures/group/subgroup/Normalizer\|Normalizer]], [[knowledge/math/algebra/structures/group/Cauchy's Theorem\|Cauchy's Theorem]], [[knowledge/math/algebra/structures/action/Group Action\|Group Action]], [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]]
