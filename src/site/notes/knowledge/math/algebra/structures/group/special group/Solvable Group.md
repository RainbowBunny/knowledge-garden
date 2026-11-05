---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/special-group/solvable-group/","dg-note-properties":{"aliases":["Soluble Group","Subnormal Series"]}}
---

Reference:
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_, §13.2 Solvable Groups, read in the LibreTexts copy: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_(Judson)/13%3A_The_Structure_of_Groups/13.02%3A_Solvable_Groups
- `[Put]` — A. Putman, _Burnside's p^a q^b-theorem_, lecture notes, University of Notre Dame, Theorem A: https://academicweb.nd.edu/~andyp/notes/BurnsidePQ.pdf

## Definition

> [!definition] Parameters
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]].

> [!definition] Subnormal Series
> A **subnormal series** of $G$ is a finite chain of subgroups
> $$G = H_n \supset H_{n-1} \supset \cdots \supset H_1 \supset H_0 = \{e\}$$
> with each $H_i$ a [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]] of $H_{i+1}$. It is a **normal series** if each $H_i$ is normal in $G$, and a **composition series** if all the factors $H_{i+1}/H_i$ are simple.
>
> `[Jud §13.2]`

> [!definition] Solvable Group
> Extends:: [[knowledge/math/algebra/structures/group/Group\|Group]].
>
> ---
> $G$ is **solvable** if it has a subnormal series whose factor groups $H_{i+1}/H_i$ are all [[knowledge/math/algebra/structures/group/special group/Abelian Group\|abelian]].
>
> `[Jud §13.2]`

## Example

> [!example] Solvable and not `[Jud §13.2]`
> - Every abelian group: $G \supset \{e\}$.
> - $S_4$: the series $S_4 \supset A_4 \supset \{e, (1\,2)(3\,4), (1\,3)(2\,4), (1\,4)(2\,3)\} \supset \{e\}$ has abelian factors.
> - $S_n$ for $n \geq 5$ is not solvable: $S_n \supset A_n \supset \{e\}$ is a composition series with the nonabelian factor $A_n$.

> [!example] Groups of order $p^a q^b$
> Every group whose order has at most two prime factors is solvable — [[knowledge/math/algebra/structures/group/special group/Burnside's Solvability Theorem\|Burnside's Solvability Theorem]] `[Put Thm A]`. $S_5$, of order $120 = 2^3 \cdot 3 \cdot 5$, shows that three primes are too many.

## Related

### Properties
- [[knowledge/math/algebra/structures/group/special group/Burnside's Solvability Theorem\|Burnside's Solvability Theorem]] — groups of order $p^a q^b$ are solvable

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]], [[knowledge/math/algebra/structures/group/special group/Quotient Group\|Quotient Group]], [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]]
