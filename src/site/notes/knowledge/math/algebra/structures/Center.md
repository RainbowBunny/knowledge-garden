---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/center/","dg-note-properties":{}}
---

Reference:
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — Exercise 3.5.48 (read at the mirror https://judsonbooks.org/aata-files/aata-html/).
- `[WP]` — Wikipedia, _Center (algebra)_: https://en.wikipedia.org/wiki/Center_(algebra) — groups, semigroups, rings.
- `[Mathlib]` — Mathlib, module `Mathlib.Algebra.Group.Center` (`Set.center`, `IsMulCentral`): https://leansearch.net/doc/Mathlib.Algebra.Group.Center.html
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Definition

> [!definition] Parameters
> - $(M, \star)$: a [[knowledge/math/algebra/structures/Magma\|Magma]] — only [[knowledge/math/property/operation/Commutativity\|Commutativity]], checked element by element, is involved.

> [!definition] Center
> Requires:: [[knowledge/math/algebra/structures/Magma\|Magma]].
>
> ---
> The **center** of $(M, \star)$ is a subset:
> $$Z(M) = \{m \in M \mid (\forall a \in M): a \star m = m \star a\}.$$
> `[Jud Ex 3.5.48]` (for a group) `[WP]` (for groups, semigroups, rings)
>
> ⚠️ CLAUDE – verify: for a magma that is not associative, Mathlib's `Set.center` ("the center of a magma") also asks $m$ to associate with all elements, i.e. for all $a, b \in M$ `[Mathlib]`:
> - $m \star (a \star b) = (m \star a) \star b$;
> - $(a \star m) \star b = a \star (m \star b)$;
> - $(a \star b) \star m = a \star (b \star m)$.
>
> On a [[knowledge/math/algebra/structures/Semigroup\|Semigroup]] the two definitions agree, so the specializations below are unaffected; decide which one this origin uses.

> [!todo] To write
> The definition over a magma, and the edge case: in an [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]] or a [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]] the center is everything.

## Related

### Descendants

| where            | what the structure adds                                                                  |
| ---------------- | ---------------------------------------------------------------------------------------- |
| [[knowledge/math/algebra/structures/ring/subring/Ring Center\|Ring Center]]  | the center of $(R, \cdot)$; it is a [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]], and for a [[knowledge/math/algebra/structures/ring/special ring/Division Ring\|Division Ring]] a [[knowledge/math/algebra/structures/field/Field\|Field]] |
| [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]] | the center of a [[knowledge/math/algebra/structures/group/Group\|Group]] is an abelian [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]]                              |
