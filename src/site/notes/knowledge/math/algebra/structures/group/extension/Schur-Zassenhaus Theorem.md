---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/extension/schur-zassenhaus-theorem/","dg-note-properties":{"aliases":["Schur–Zassenhaus Theorem"]}}
---

Reference:
- `[ConSZ]` — K. Conrad, _The Schur–Zassenhaus theorem_, expository notes, Theorem 1, Remark 5: https://kconrad.math.uconn.edu/blurbs/grouptheory/schurzass.pdf

## Definition

> [!theorem] Schur-Zassenhaus Theorem — a normal subgroup of order prime to its index has a complement
> ### Scope
> - $G$: a finite [[knowledge/math/algebra/structures/group/Group\|Group]] with $|G| = ab$, $\gcd(a, b) = 1$.
> - $N \trianglelefteq G$: a [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]] of order $a$.
>
> ---
> ### Condition
> - $\gcd(a, b) = 1$.
>
> ---
> ### Property
> $G$ has a subgroup $H$ of order $b$. Then $N \cap H = \{e\}$ and $G = NH$, so
> $$G \cong N \rtimes H.$$
>
> `[ConSZ Thm 1]`; the [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]] form by recognition.

## Property

> [!remark] Conjugacy of complements `[ConSZ Rem 5]`
> The second part of the theorem says that any two subgroups of order $b$ in $G$ are conjugate. Conrad omits its proof and cites D. J. S. Robinson, _A Course in the Theory of Groups_, pp. 254–255.

> [!remark] In the language of extensions
> Every extension $1 \to N \to G \to Q \to 1$ with $\gcd(|N|, |Q|) = 1$ splits ([[knowledge/math/algebra/structures/group/extension/Short Exact Sequence of Groups#Splitting\|Short Exact Sequence of Groups#Splitting]], [[knowledge/math/algebra/structures/group/extension/Group Extension\|Group Extension]]).

## Example

> [!example] A normal Sylow subgroup
> A normal [[knowledge/math/algebra/structures/group/subgroup/Sylow Subgroup\|Sylow Subgroup]] $P$ has order prime to its index, so $G \cong P \rtimes H$ with $|H| = [G : P]$. For $|G| = pqr$ with $p < q < r$, the Sylow $r$-subgroup $R$ is normal, so $G \cong C_r \rtimes H$ with $|H| = pq$ — [[knowledge/math/algebra/structures/group/classification/Groups of Order pqr\|Groups of Order pqr]].

## Related

### Prerequisites
- [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]], [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]], [[knowledge/math/algebra/structures/group/extension/Group Extension\|Group Extension]]
