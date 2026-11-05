---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/special-group/burnside-s-solvability-theorem/","dg-note-properties":{"aliases":["Burnside's p^a q^b Theorem","Burnside's paqb Theorem"]}}
---

Reference:
- `[Put]` — A. Putman, _Burnside's p^a q^b-theorem_, lecture notes, University of Notre Dame, Theorem A, Lemmas 0.2, 0.3, Proposition 0.4: https://academicweb.nd.edu/~andyp/notes/BurnsidePQ.pdf
- `[Bur04]` — W. Burnside, _On groups of order p^α q^β_, Proc. London Math. Soc. (2) 1 (1904), 388–392 — the original, as cited by `[Put]`; not read.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_, §13.2 Solvable Groups, read in the LibreTexts copy: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_(Judson)/13%3A_The_Structure_of_Groups/13.02%3A_Solvable_Groups

## Definition

> [!theorem] Burnside's Solvability Theorem — a group of order $p^a q^b$ is solvable
> ### Scope
> - $p, q$: [[knowledge/math/number theory/Prime\|primes]].
> - $a, b \geq 0$: integers.
> - $G$: a finite [[knowledge/math/algebra/structures/group/Group\|Group]] with $|G| = p^a q^b$.
>
> ---
> ### Condition
> - None beyond the order: $p = q$ is allowed, and gives a [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]].
>
> ---
> ### Property
> $G$ is [[knowledge/math/algebra/structures/group/special group/Solvable Group\|solvable]].
>
> `[Put Thm A]`

## Property

> [!remark] How it is proved `[Put]`
> The key step is a nontrivial proper normal subgroup, after which induction on $|G|$ applies. It comes from character theory: matrix entries of representations are algebraic integers, which gives that $|\mathrm{cl}(g)|\, \chi(g) / \chi(1)$ is an algebraic integer (Lemma 0.3). A conjugacy class of prime-power size greater than 1 then yields a normal subgroup (Prop 0.4), and such a class exists: take a nontrivial central element of a Sylow $q$-subgroup, whose centralizer contains that subgroup.

> [!remark] Not three primes
> $S_5$ has order $2^3 \cdot 3 \cdot 5$ and is not solvable `[Jud §13.2]`.

## Example

> [!example] Which orders it covers
> - Groups of order $pq$ or $p^2 q$, such as 6, 12, 18, 20, are solvable by the theorem.
> - [[knowledge/math/algebra/structures/group/classification/Groups of Order 30\|Groups of Order 30]] have three prime factors, so the theorem does not apply. They are solvable for another reason: each has a normal cyclic subgroup of index 2.

## Related

### Prerequisites
- [[knowledge/math/algebra/structures/group/special group/Solvable Group\|Solvable Group]], [[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems\|Sylow Theorems]], [[knowledge/math/algebra/structures/action/Group Representation\|Group Representation]]
