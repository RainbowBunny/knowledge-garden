---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/cauchy-s-theorem/","dg-note-properties":{"aliases":["Cauchy's Theorem for Groups"]}}
---

Reference:
- `[ConCau]` — K. Conrad, _Cauchy's theorem_, expository notes: https://kconrad.math.uconn.edu/blurbs/grouptheory/cauchypf.pdf
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_, HTML edition, §15.1: Theorem 15.1.1, Corollary 15.1.2: https://judsonbooks.org/aata-files/aata-html/sylow-section-sylow-theorems.html (result numbers as there).

## Definition

> [!theorem] Cauchy's Theorem — a prime dividing $|G|$ is the order of some element
> ### Scope
> - $G$: a finite [[knowledge/math/algebra/structures/group/Group\|Group]].
> - $p$: a [[knowledge/math/number theory/Prime\|Prime]] dividing $|G|$.
>
> ---
> ### Condition
> - None: $G$ need not be abelian.
>
> ---
> ### Property
> $G$ contains an element of order $p$; equivalently, a subgroup of order $p$.
>
> `[ConCau]` `[Jud Thm 15.1.1]`

## Property

> [!proof] Why — induction on $|G|$
> For abelian $G$, Conrad maps a product of cyclic groups onto $G$ and uses the first isomorphism theorem. For nonabelian $G$, the [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]] $|G| = |Z(G)| + \sum_i [G : C_G(g_i)]$ gives either a proper centralizer $C_G(g_i)$ of order divisible by $p$, where induction applies, or $p \mid |Z(G)|$ and the abelian case applies `[ConCau]`. For $p = 2$, pairing each $g$ with $g^{-1}$ leaves an even number of elements with $g = g^{-1}$, one of them $e$ `[ConCau]`.

> [!corollary] $p$-groups — a finite group is a $p$-group iff its order is a power of $p$
> **Scope**
> - $G$: a finite group.
>
> ---
> **Property**
> Every element of $G$ has $p$-power order iff $|G| = p^n$ for some $n$.
>
> `[Jud Cor 15.1.2]`: if a second prime $q$ divided $|G|$, Cauchy would give an element of order $q$. See [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]].

## Example

> [!example] The converse of Lagrange fails beyond primes
> Cauchy gives subgroups for prime divisors only. The alternating group $A_4$, of order 12, has no subgroup of order 6, although $6 \mid 12$; the [[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems\|Sylow Theorems]] add the prime-power divisors.

## Related

### Constructions
- [[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems\|Sylow Theorems]] — the existence proof extends a $p$-subgroup by a subgroup of order $p$ from Cauchy

### Prerequisites
- [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]], [[knowledge/math/algebra/structures/group/subgroup/Subgroup#Property\|Subgroup#Property]] (Lagrange's theorem)
