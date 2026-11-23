---
{"dg-publish":true,"permalink":"/knowledge/math/property/relation/connexity/","dg-note-properties":{}}
---

Reference:
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definitions rel.7, rel.16: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3.

## Definition

> [!definition] Connexity (Totality)
> ### Scope
> A relation $R \subseteq O \times O$.
> 
> ---
> ### Property
> A relation $R$ is connex iff 
> $$\forall x, y \in O: (x \;R\; y) \lor (y \;R\; x)$$

## Property

> [!remark] Connexity is not Munkres's comparability
> Taking $y = x$ gives $x \,R\, x$: connexity implies [[knowledge/math/property/relation/Reflexivity\|Reflexivity]]. So a strict order, which is [[knowledge/math/property/relation/Irreflexivity\|irreflexive]], is never connex on a nonempty set. The condition strict orders use, $x \neq y \Rightarrow x \,R\, y \lor y \,R\, x$, is [[knowledge/math/property/relation/Comparability\|Comparability]]: `[Mun00 §3]`'s word, `[OLP-Rel Def rel.7]`'s "connected". Connexity is comparability plus reflexivity ([[knowledge/math/property/relation/Comparability#Property\|Comparability#Property]]), which is why `[OLP-Rel Def rel.16]` can define a total order with the weaker condition.

## Related

### Descendants
- [[knowledge/math/set theory/order/Total Order\|Total Order]] — connex, antisymmetric, transitive

### Siblings
- [[knowledge/math/property/relation/Comparability\|Comparability]] — the $x \neq y$ version, used by strict orders
