---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/class/time/class-np-intermediate/","dg-note-properties":{"aliases":["NP-Intermediate","NPI"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 3: Diagonalization, Section 3.3: Ladner's Theorem: Existence of NP-Intermediate Problems, Theorem 3.3, p. 71.

## Intuition

> [!intuition] Why
> If P ≠ NP, is every NP problem either easy or as hard as SAT? Ladner's theorem says no. NP-intermediate problems are where factoring and graph isomorphism are believed to live, which is how cryptography can rest on factoring without factoring being NP-complete.

## Definition

> [!definition] Class NP-Intermediate
> Requires:: [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]], [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]]
>
> ---
> A language is **NP-intermediate** iff it is in [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]], not in [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], and not NP-complete under [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Karp reductions]]:
> $$\mathsf{NPI} = \mathsf{NP} \setminus (\mathsf P \cup \mathsf{NP}\text{-complete}).$$
> `[AB09 §3.3]`

## Property

> [!theorem] Nonempty exactly when P ≠ NP
> **Scope**
> - $\mathsf{NPI}$.
>
> ---
> **Property**
> $\mathsf{NPI} \neq \emptyset \iff \mathsf P \neq \mathsf{NP}$.
>
> ⇐ is [[knowledge/complexity/theorem/Ladner's Theorem\|Ladner's Theorem]]. ⇒: if $\mathsf P = \mathsf{NP}$, then $\mathsf{NP} \setminus \mathsf P = \emptyset$.

## Example

> [!example] Candidates
> [[knowledge/complexity/problem/number/Factoring\|Factoring]] and [[knowledge/complexity/problem/graph/Graph Isomorphism\|Graph Isomorphism]] are in $\mathsf{NP}$, are not known to be in $\mathsf P$, and are believed not to be NP-complete.

## Related

### Prerequisites
- [[knowledge/complexity/theorem/Ladner's Theorem\|Ladner's Theorem]]
