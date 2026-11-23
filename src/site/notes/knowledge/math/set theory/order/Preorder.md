---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/preorder/","dg-note-properties":{"aliases":["Quasiorder"]}}
---

Reference:
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definition rel.14: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf

## Definition

> [!definition] Preorder (Quasiorder)
> A [[knowledge/math/set theory/relation/Relation\|Relation]] $\leq$ on a set $S$ is called a preorder (or quasiorder) if it satisfies
> - [[knowledge/math/property/relation/Reflexivity\|Reflexivity]];
> - [[knowledge/math/property/relation/Transitivity\|Transitivity]].
>
> `[OLP-Rel Def rel.14]`

## Property

> [!proposition] Quotient — a preorder is a partial order on its classes
> **Scope**
> - $\leq$ a preorder on $S$.
>
> ---
> **Property**
> $a \sim b \iff a \leq b \land b \leq a$ is an [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]].
> $[a] \leq [b] \iff a \leq b$ is a well-defined [[knowledge/math/set theory/order/Partial Order\|Partial Order]] on $S/{\sim}$.
>
> $\sim$ is symmetric by its form and inherits reflexivity and transitivity. If $a \sim a'$ and $b \sim b'$, then $a \leq b$ gives $a' \leq a \leq b \leq b'$, so the induced relation does not depend on representatives; it is antisymmetric because $[a] \leq [b] \leq [a]$ means $a \sim b$.

## Example

> [!example] Divisibility on $\mathbb Z$
> $a \mid b$ is a preorder on $\mathbb Z$ that is not antisymmetric: $2 \mid -2$ and $-2 \mid 2$. Its classes are the sets $\{n, -n\}$, and the quotient order is divisibility on $\mathbb Z_{\geq 0}$.

## Related

### Descendants
- [[knowledge/math/set theory/order/Partial Order\|Partial Order]] — adds [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]]

### Siblings
- [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] — adds [[knowledge/math/property/relation/Symmetry\|Symmetry]] instead
