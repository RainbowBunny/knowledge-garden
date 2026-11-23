---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/action/orbit/","dg-note-properties":{}}
---

Reference:
- `[Alu09]` — P. Aluffi, _Algebra: Chapter 0_, Graduate Studies in Mathematics 104, American Mathematical Society, 2009, Chapter II: Groups, first encounter, Section 9.1: Actions; Section 9.2: Actions on sets; Chapter IV: Groups, second encounter, Section 1.1: Actions of groups on sets, reminder.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the LibreTexts copy, item numbers as there: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_%28Judson%29), §14.1 Groups Acting on Sets; §14.2 The Class Equation.

## Definition

> [!definition] Parameters
> - [[knowledge/math/algebra/structures/action/Group Action\|Group Action]]: Import $(G, A, \rho)$, writing $ga = \rho(g, a)$.
> - $a \in A$: an element.

> [!definition] Orbit
> Requires:: [[knowledge/math/algebra/structures/action/Group Action\|Group Action]].
>
> ---
> The **orbit** of $a \in A$ under an action of a [[knowledge/math/algebra/structures/group/Group\|Group]] $G$ is the [[knowledge/math/set theory/Set\|Set]]
> $$O_G(a) = \{ga \mid g \in G\}.$$
> `[Alu09 II.9.2]` `[Jud §14.1]`

### Trivial Orbit

> [!definition] Trivial Orbit
> The orbit of $a$ is 'trivial' if $|O_G(a)| = 1$. `[Alu09 IV.1.1]` `[Jud §14.2]`

## Related

### Prerequisites
- [[knowledge/math/algebra/structures/action/Group Action\|Group Action]] — the action whose orbits these are

### Siblings
- [[knowledge/math/algebra/structures/action/Stabilizer\|Stabilizer]] — the subgroup fixing $a$; the orbit–stabilizer theorem relates the two
