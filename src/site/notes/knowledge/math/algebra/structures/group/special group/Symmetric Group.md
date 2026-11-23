---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/special-group/symmetric-group/","dg-note-properties":{}}
---

Reference:
- `[Alu09]` — P. Aluffi, _Algebra: Chapter 0_, Graduate Studies in Mathematics 104, American Mathematical Society, 2009, Chapter II: Groups, first encounter, Section 2.1: Symmetric Groups.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the HTML edition at https://judsonbooks.org/aata-files/aata-html/; result numbers as there).

## Definition

> [!definition] Parameters
> - $A$: a [[knowledge/math/set theory/Set\|Set]].
> - $n$: a positive integer.

> [!definition] Symmetric Group
> Instantiates:: [[knowledge/math/algebra/structures/group/Group\|Group]].
>
> ---
> Let $A$ be a set. The **symmetric group**, or **group of permutations** of $A$, denoted $S_A$, is the group $\mathsf{Aut}_\mathsf{Set}(A)$. The group of permutations of the set $\{1, \dots, n\}$ is denoted by $S_n.$ `[Alu09 II §2.1]` `[Jud §5.1]`

## Property

> [!proposition] Order of $S_n$ — $|S_n| = n!$
> $S_n$ is a group with $n!$ elements under composition of maps. `[Jud Thm 5.1.1]`

## Related

### Constructions
- [[knowledge/math/algebra/structures/action/Group Action\|Group Action]] — every group acts faithfully on some set, so embeds in some $S_A$ (Cayley's theorem — every group is isomorphic to a group of permutations `[Jud Thm 9.1.12]`)

### Prerequisites
- [[knowledge/math/property/map/Bijection\|Bijection]] — the elements of $S_A$
- [[knowledge/math/algebra/category/example/Category Set\|Category Set]] — $\mathsf{Aut}_\mathsf{Set}(A)$
