---
{"dg-publish":true,"permalink":"/knowledge/complexity/theorem/ladner-s-theorem/","dg-note-properties":{"aliases":["Ladner Theorem","Existence of NP-Intermediate Problems"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 3: Diagonalization, Section 3.3: Ladner's Theorem: Existence of NP-Intermediate Problems, Theorem 3.3, p. 71.

## Intuition

> [!intuition] Why
> It shows that P ≠ NP would not split NP into just the easy problems and the complete ones. That is why a problem like factoring can be hard without being NP-complete.

## Definition

> [!theorem] Ladner's Theorem — if P ≠ NP, NP has problems of intermediate difficulty
> ### Scope
> - [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]].
>
> ---
> ### Condition
> - $\mathsf P \neq \mathsf{NP}$.
>
> ---
> ### Property
> There is a [[knowledge/computability/language/Language\|Language]] $L \in \mathsf{NP} \setminus \mathsf P$ that is not [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|NP-complete]].
>
> `[AB09 Thm 3.3]`

## Property

> [!proof] Why — SAT padded by a slowly growing amount
> Define $\mathsf{SAT}_H = \{\psi\, 0\, 1^{n^{H(n)}} : \psi \in \mathsf{SAT},\ |\psi| = n\}$, where $H(n)$ is computed by diagonalization: the least $i < \log \log n$ such that the $i$-th machine $M_i$ decides $\mathsf{SAT}_H$ correctly, within $i |x|^i$ steps, on all inputs of length at most $\log n$; and $\log \log n$ if there is none. Then $\mathsf{SAT}_H \in \mathsf{NP}$, and:
> - If $\mathsf{SAT}_H \in \mathsf P$, then $H$ is bounded by a constant, the padding is polynomial, and $\mathsf{SAT} \in \mathsf P$.
> - If $\mathsf{SAT}_H$ is NP-complete, then $H(n) \to \infty$, so the padding is super-polynomial, and a reduction from $\mathsf{SAT}$ to $\mathsf{SAT}_H$ maps formulas to much shorter formulas; iterating it decides $\mathsf{SAT}$ in polynomial time.
>
> Either way $\mathsf P = \mathsf{NP}$. `[AB09 §3.3]`

> [!remark] The converse is trivial
> If $\mathsf P = \mathsf{NP}$, every nontrivial language in $\mathsf{NP}$ is NP-complete, so no intermediate language exists: [[knowledge/complexity/complexity class/class/time/Class NP-Intermediate\|Class NP-Intermediate]] is nonempty exactly when $\mathsf P \neq \mathsf{NP}$.

## Example

> [!example] Natural candidates
> The language $\mathsf{SAT}_H$ is artificial. No natural problem is known to be NP-intermediate under $\mathsf P \neq \mathsf{NP}$, but [[knowledge/complexity/problem/number/Factoring\|Factoring]] and [[knowledge/complexity/problem/graph/Graph Isomorphism\|Graph Isomorphism]] are believed to be: they are in $\mathsf{NP}$, no polynomial algorithm is known, and there is evidence against their NP-completeness.

## Related

### Siblings
- [[knowledge/complexity/theorem/Nondeterministic Time Hierarchy Theorem\|Nondeterministic Time Hierarchy Theorem]] — the same technique of lazy diagonalization

### Prerequisites
- [[knowledge/complexity/complexity class/class/time/Class NP-Intermediate\|Class NP-Intermediate]], [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]], [[knowledge/complexity/problem/logic/Satisfiability\|Satisfiability]]
