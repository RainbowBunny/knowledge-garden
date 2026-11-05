---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/action/class-equation/","dg-note-properties":{"aliases":["Class Formula","Conjugacy Class"]}}
---

Reference:
- `[ConConj]` — K. Conrad, _Conjugation in a group_, expository notes, §2, equation (6.4), Theorems 6.7–6.9, Corollary 6.11: https://kconrad.math.uconn.edu/blurbs/grouptheory/conjclass.pdf

## Definition

> [!theorem] Class Equation — $|G|$ is $|Z(G)|$ plus the sizes of the nontrivial conjugacy classes
> ### Scope
> - $G$: a finite [[knowledge/math/algebra/structures/group/Group\|Group]], with [[knowledge/math/algebra/structures/group/subgroup/Group Center\|center]] $Z(G)$.
> - $g_1, \dots, g_r$: one element from each conjugacy class with more than one element.
>
> ---
> ### Condition
> - None.
>
> ---
> ### Property
> $$|G| = |Z(G)| + \sum_{i=1}^r [G : C_G(g_i)],$$
> where each $[G : C_G(g_i)] > 1$ divides $|G|$ ([[knowledge/math/algebra/structures/group/subgroup/Centralizer\|Centralizer]]).
>
> `[ConConj (6.4), Thm 6.7]`

> [!remark] Conjugacy class
> The **conjugacy class** of $g \in G$ is $\{xgx^{-1} \mid x \in G\}$, the [[knowledge/math/algebra/structures/action/Orbit\|Orbit]] of $g$ under conjugation ([[knowledge/math/algebra/structures/action/example/Group Action on Group\|Group Action on Group]]). The conjugacy classes partition $G$; the classes with one element are the elements of $Z(G)$.
>
> `[ConConj §2]`

## Property

> [!remark] An orbit decomposition
> The class equation is the [[knowledge/math/algebra/structures/action/Group Action#Property\|orbit decomposition]] for $G$ acting on itself by conjugation: the fixed points are $Z(G)$, and the orbit of $g$ has $[G : C_G(g)]$ elements by the orbit–stabilizer theorem ([[knowledge/math/algebra/structures/action/Stabilizer#Property\|Stabilizer#Property]]).

> [!corollary] Consequences for $p$-groups `[ConConj Thm 6.8, Thm 6.9, Cor 6.11]`
> - A nontrivial finite $p$-group has a nontrivial center.
> - A nontrivial normal subgroup of a nontrivial finite $p$-group meets the center nontrivially.
> - Every group of order $p^2$ is abelian.
>
> See [[knowledge/math/algebra/structures/group/special group/p-Group#Property\|p-Group#Property]] and [[knowledge/math/algebra/structures/group/classification/Groups of Order p²\|Groups of Order p²]].

## Example

> [!example] $S_3$
> $|S_3| = 6 = 1 + 2 + 3$: the center is $\{e\}$, the 3-cycles form a class of size 2, and the transpositions a class of size 3.

## Related

### Constructions
- [[knowledge/math/algebra/structures/group/Cauchy's Theorem\|Cauchy's Theorem]] — proved by induction from the class equation
- [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]] — the center of a nontrivial $p$-group is nontrivial

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Centralizer\|Centralizer]], [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]], [[knowledge/math/algebra/structures/action/example/Group Action on Group\|Group Action on Group]], [[knowledge/math/algebra/structures/action/Stabilizer\|Stabilizer]]
