---
{"dg-publish":true,"permalink":"/knowledge/math/property/relation/asymmetry/","dg-note-properties":{"aliases":["Asymmetric"]}}
---

Reference:
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definitions rel.9, rel.22: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf

## Definition

> [!definition] Asymmetry
> ### Scope
> A relation $R \subseteq O \times O$.
>
> ---
> ### Property
> $R$ is **asymmetric** iff
> $$\forall x, y \in O: x \;R\; y \Rightarrow \neg (y \;R\; x)$$
>
> `[OLP-Rel Def rel.9]`

## Property

> [!proposition] Asymmetry — irreflexive plus antisymmetric
> **Scope**
> - $R \subseteq O \times O$.
>
> ---
> **Property**
> $R$ is asymmetric $\iff$ $R$ satisfies [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]] and [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]].
>
> ⇒: taking $y = x$ gives irreflexivity, and $x \,R\, y \land y \,R\, x$ never happens, so antisymmetry holds vacuously. ⇐: if $x \,R\, y$ and $y \,R\, x$, antisymmetry gives $x = y$, so $x \,R\, x$, against irreflexivity.

## Example

> [!example] In the definition of a strict order
> `[OLP-Rel Def rel.22]` lists asymmetry among the axioms of a strict order. For a transitive relation it is redundant, since irreflexivity and transitivity imply it ([[knowledge/math/property/relation/Irreflexivity#Property\|Irreflexivity#Property]]).

> [!example] Where it fails
> $\leq$ on $\mathbb R$ is antisymmetric but not asymmetric: $1 \leq 1$.

## Related

### Siblings
- [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]] — allows $x \,R\, x$; asymmetry forbids it
- [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]] — implied by asymmetry
