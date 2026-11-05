---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/function/canonical-decomposition/","dg-note-properties":{}}
---

Reference:
- [[academic/Book Reference\|Algebra: Chapter 0]] - Chapter II: Groups, first encounter, Section 8.1: Canonical decomposition.
- [[academic/Book Reference\|Algebra: Chapter 0]] - Chapter III: Rings and modules, Section 3.3: Canonical decomposition and consequences.

## Definition

The relation defined here is the [[knowledge/math/set theory/function/Kernel\|knowledge/math/set theory/function/Kernel]] of $f$ — it belongs in that note; the decomposition is the theorem below.

> [!definition] Canonical Decomposition
> A canonical decomposition is a [[knowledge/math/set theory/Function\|Function]] $f: A \rightarrow B$ determines an [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] $\sim$ on $A$ as follows:
> - For all $a', a'' \in A$,
> $$a' \sim a'' \Longleftrightarrow f(a') = f(a'')$$

## Property

### For Set Function

> [!theorem]
> Let $f: A \rightarrow B$ be any function, and define $\sim$ as above. Then $f$ decomposes as follows:
> $$A \twoheadrightarrow (A/_\sim) \; \substack{\sim \\ \longrightarrow \\ \tilde f} \; \text{im} f \hookrightarrow B$$
> where the first function is the canonical projection, the third function is the inclusion $\text{im} \; f \subseteq B$, and the bijection $\tilde f$ in the middle is defined by
> $$\tilde f([a]_\sim) = f(a)$$
> for all $a \in A$.

### For Group Homomorphism

> [!theorem]
> Every [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] $\varphi: G \rightarrow G'$ may be decomposed as follows:
> $$G \twoheadrightarrow G / \ker{\varphi} \xrightarrow[\tilde{\varphi}]{\sim} \mathrm{im}\;{\varphi} \hookrightarrow G'$$
> 
> ---
> This $\tilde{\varphi}$ is the unique homomorphism induced by $\varphi$ in [[knowledge/math/algebra/structures/group/special group/Quotient Group\|Universal Property of the Quotient]].

### For Ring Homomorphism

> [!theorem]
> Every [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]] $\varphi: R \rightarrow S$ may be decomposed as follows:
> $$R \twoheadrightarrow R / \ker{\varphi} \xrightarrow[\tilde{\varphi}]{\sim} \mathrm{im}\;{\varphi} \hookrightarrow S$$ 
