---
{"dg-publish":true,"permalink":"/knowledge/math/foundations-of-mathematics/","dg-note-properties":{}}
---

Reference:
- https://en.wikipedia.org/wiki/Foundations_of_mathematics
- https://en.wikipedia.org/wiki/Class_(set_theory)

## Intuition

What everything else silently stands on — and the honest note is short, because this vault (like working mathematics) does not depend on the choice. Foundations become visible only at a few boundaries; this note is the register of those boundaries.

## The default

> [!remark] ZFC, unexamined
> The background theory is ZFC, as for most of mathematics — and nothing in this vault depends on which foundation is chosen; type-theoretic foundations power proof assistants, and the content translates. See the coexistence rules in [[North Star\|North Star]].

## Class vs Set — the boundary the vault has already met

> [!definition] Class, Proper Class
> A **class** is a collection defined by a shared property. A **proper class** is a class that is not a set. The class of all sets $V$, the class of all ordinals, and Russell's class $\{x : x \notin x\}$ are proper — Russell's paradox ([[knowledge/math/set theory/Set Foundation\|Set Foundation]]) is exactly the proof for the last one.

> [!remark] Where it bites here
> $\mathsf{Obj}(\mathbf{Set})$ and $\mathsf{Obj}(\mathbf{Grp})$ are proper classes — which is why [[knowledge/math/algebra/category/Category\|Category]] needs *small* / *locally small*, and why "the category of all categories" needs care. ZFC handles classes as informal shorthand; NBG makes them first-class objects. For this vault, the remark in [[knowledge/math/algebra/category/Category\|Category]] suffices.

## Axiom of Choice — noted, not needed

> [!remark]
> AC is equivalent to Zorn's lemma, which gives maximal ideals in every [[knowledge/math/algebra/structures/ring/Ring\|Ring]] and bases in every [[knowledge/math/algebra/linear algebra/Vector Spaces\|vector space]]. Everything cryptographic in this vault is finite or countable, where AC is silent. Flag it if a note ever invokes Zorn; otherwise it stays here.