---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/operator/hardness-and-completeness/","dg-note-properties":{"aliases":["NP-hard","NP-complete","Hardness","Completeness","C-hard","C-complete"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.2: Reducibility and NP-completeness, Definition 2.7, p. 42, Theorems 2.8, 2.9, p. 43; Chapter 4: Space complexity, Section 4.3: NL Completeness.

## Intuition

> [!intuition] Why
> A complete problem captures its whole class: solve it efficiently and every problem in the class is solved. That turns a question about classes, such as P versus NP, into a question about one problem, such as SAT.

## Definition

> [!definition] Hardness and Completeness
> ### Scope
> A [[knowledge/complexity/complexity class/Complexity Class\|Complexity Class]] $\mathsf{C}$ and a reducibility $\leq$.
> 
> ---
> ### Property
> - $L$ is **$\mathsf C$-hard** iff $A \leq L$ for every $A \in \mathsf C$.
> - $L$ is **$\mathsf C$-complete** iff $L$ is $\mathsf C$-hard and $L \in \mathsf C$.
>
> `[AB09 Def 2.7]` for $\mathsf C = \mathsf{NP}$ with [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]].

> [!remark] Which reduction goes with which class
> | completeness | reduction |
> | --- | --- |
> | NP-complete, coNP-complete, PSPACE-complete, EXP-complete | [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]] |
> | NL-complete, P-complete | [[knowledge/complexity/complexity class/reducibility/Log-space Reducibility\|Log-space Reducibility]] |

## Property

> [!proposition] Hardness transfers along reductions
> **Scope**
> - $\leq$ transitive; $L$ $\mathsf C$-hard; $L \leq L'$.
>
> ---
> **Property**
> $L'$ is $\mathsf C$-hard.
> If $L$ lies in a class $\mathsf C'$ closed under $\leq$, then $\mathsf C \subseteq \mathsf C'$.
>
> `[AB09 Thm 2.8]`. For $\mathsf C = \mathsf{NP}$, $\mathsf C' = \mathsf P$: an NP-hard language in $\mathsf P$ gives $\mathsf P = \mathsf{NP}$.

> [!remark] Why the reduction must be weaker than the class
> A reduction that is allowed to do as much as the class can **decide** the source language itself and output a fixed yes- or no-instance. With polynomial-time reductions, every nontrivial language in $\mathsf P$ would be P-complete, and every nontrivial language in $\mathsf{NL}$ would be NL-complete, so these notions would say nothing. Log-space reductions are weak enough to keep them meaningful `[AB09 §4.3]`.

## Example

> [!example] The first complete problems
> - NP-complete: [[knowledge/complexity/problem/logic/Satisfiability\|SAT]] and [[knowledge/complexity/problem/logic/3Satisfiability\|3SAT]], by the [[knowledge/complexity/theorem/Cook-Levin Theorem\|Cook-Levin Theorem]]; [[knowledge/complexity/problem/machine/Turing Machine Satisfiability\|TMSAT]], directly from the definition `[AB09 Thm 2.9]`.
> - coNP-complete: [[knowledge/complexity/problem/logic/Tautology\|TAUTOLOGY]].
> - PSPACE-complete: [[knowledge/complexity/problem/logic/True Quantified Boolean Formula\|TQBF]].
> - NL-complete: [[knowledge/complexity/problem/graph/Vertex Path\|PATH]].

## Related

### Instantiations
- [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]], [[knowledge/complexity/complexity class/reducibility/Log-space Reducibility\|Log-space Reducibility]], [[knowledge/complexity/complexity class/reducibility/Randomized Polynomial Reducibility\|Randomized Polynomial Reducibility]] — the reducibilities used

### Siblings
- [[knowledge/complexity/complexity class/class/time/Class NP-Intermediate\|Class NP-Intermediate]] — in $\mathsf{NP}$, but neither easy nor complete
