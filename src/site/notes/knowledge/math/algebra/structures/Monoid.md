---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/monoid/","dg-note-properties":{}}
---

Reference:
- `[AAN]` — _Abstract Algebra_ (unattributed lecture notes): https://pages.physics.ua.edu/faculty/fabi/CT/AbstractAlgebra.pdf
- `[BS81]` — S. Burris, H. P. Sankappanavar, _A Course in Universal Algebra_ (1981; Millennium Edition): https://math.uwaterloo.ca/~snburris/htdocs/ualg.html — Chapter II, §1, Examples (read at https://people.math.sc.edu/mcnulty/alglatvar/burrissanka.pdf).
- `[Lei]` — T. Leinster, _Basic Category Theory_ (2014), arXiv:1612.09375 — Example 1.1.8(d).
- `[Rie]` — E. Riehl, _Category Theory in Context_ (2016): https://math.jhu.edu/~eriehl/context.pdf — Example 1.1.4(ii) and its footnote 9 (read at the mirror https://www.math.ucla.edu/~mopie/context.pdf).

## Definition

> [!definition] Parameters
> - $M$: a [[knowledge/math/set theory/Set\|Set]].
> - $\circ$: a [[knowledge/math/set theory/operation/Binary Operation\|Binary Operation]] on $M$.

> [!definition] Monoid
> Extends:: [[knowledge/math/algebra/structures/Semigroup\|Semigroup]].
>
> ---
> A **monoid** is a set $M$ together with a binary operation $\circ$ that satisfies [[knowledge/math/property/operation/Closure\|Closure]], [[knowledge/math/property/operation/Associativity\|Associativity]], [[knowledge/math/property/operation/Identity Element\|Identity Element]]. `[AAN]` `[BS81 II §1]` `[Lei Ex 1.1.8(d)]`

> [!definition] Monoid (Alternative)
> Alternatively, a **monoid** is a [[knowledge/math/algebra/structures/Semigroup\|Semigroup]] whose binary operation $\circ$ satisfies [[knowledge/math/property/operation/Identity Element\|Identity Element]]. `[AAN]`

## Property

> [!proposition] Monoids are one-object categories — a monoid is the same as a category with a single object
> A monoid $M$ defines a [[knowledge/math/algebra/category/Category\|Category]] with a single object, whose morphisms are the elements of $M$ and whose composition is $\circ$; equivalently, a monoid is a one-object category. `[Rie Ex 1.1.4(ii)]` `[Lei Ex 1.1.8(d)]`

## Related

### Descendants
- [[knowledge/math/algebra/structures/group/Group\|Group]] — adds an [[knowledge/math/property/operation/Inverse Element\|Inverse Element]] for every element.

### Constructions
- [[knowledge/math/algebra/structures/ring/example/Monoid Ring\|Monoid Ring]] — the ring $R[M]$ built from a ring $R$ and a monoid $M$.
