---
{"dg-publish":true,"permalink":"/knowledge/math/property/relation/irreflexivity/","dg-note-properties":{"aliases":["Nonreflexivity","Irreflexive"]}}
---

Reference:
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definition rel.8: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3 (order relation, "nonreflexivity"); §11 (strict partial order).
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, Definition 2.1(i), read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf

## Definition

> [!definition] Irreflexivity
> ### Scope
> A relation $R \subseteq O \times O$.
>
> ---
> ### Property
> $R$ is **irreflexive** iff
> $$\forall x \in O: \neg (x \;R\; x)$$
>
> `[OLP-Rel Def rel.8]`, `[Jec03 Def 2.1(i)]`; `[Mun00 §3]` calls it **nonreflexivity**.

## Property

> [!proposition] Asymmetry — follows from irreflexivity and transitivity
> **Scope**
> - $R \subseteq O \times O$ satisfying Irreflexivity and [[knowledge/math/property/relation/Transitivity\|Transitivity]].
>
> ---
> **Property**
> $R$ satisfies [[knowledge/math/property/relation/Asymmetry\|Asymmetry]].
>
> If $x \,R\, y$ and $y \,R\, x$, transitivity gives $x \,R\, x$, which irreflexivity forbids. This is why `[Mun00 §11]` and `[Jec03 Def 2.1]` define a strict order by these two axioms alone.

## Example

> [!example] Where it holds and where it fails
> - $<$ on $\mathbb R$ and proper inclusion $\subsetneq$ on a set of sets are irreflexive.
> - Irreflexive is not the negation of [[knowledge/math/property/relation/Reflexivity\|Reflexivity]]: on $O = \{a, b\}$, $R = \{(a, a)\}$ is neither.
> - On a nonempty $O$ no relation is both reflexive and irreflexive; on $O = \emptyset$ the empty relation is both.

## Related

### Descendants
- [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]] — irreflexive and transitive

### Siblings
- [[knowledge/math/property/relation/Reflexivity\|Reflexivity]] — the opposite demand on the diagonal
- [[knowledge/math/property/relation/Asymmetry\|Asymmetry]] — implies irreflexivity: take $y = x$
