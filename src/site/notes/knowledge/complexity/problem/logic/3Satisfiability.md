---
{"dg-publish":true,"permalink":"/knowledge/complexity/problem/logic/3-satisfiability/","dg-note-properties":{"aliases":["3SAT","3CNF Satisfiability"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.3.2: The Cook-Levin Theorem, Lemma 2.14, p. 49.

## Definition

> [!definition] 3SAT
> $$\mathsf{3SAT} = \{\varphi : \varphi \text{ is a satisfiable 3CNF formula}\}$$
> with 3CNF as in [[knowledge/complexity/problem/logic/Satisfiability#Definition\|Satisfiability#Definition]]. `[AB09 §2.3]`

## Property

> [!theorem] Status — NP-complete
> Requires:: [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]]
> Complete for:: [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]] under [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]]
> 
> ---
> $\mathsf{3SAT}$ is NP-complete: the [[knowledge/complexity/theorem/Cook-Levin Theorem\|Cook-Levin Theorem]], via $\mathsf{SAT} \leq_p \mathsf{3SAT}$ `[AB09 Lemma 2.14]`.

> [!remark] Where the line is
> $\mathsf{2SAT}$, with at most two literals per clause, is in [[knowledge/complexity/complexity class/class/time/Class P\|Class P]]; three literals per clause is where NP-completeness starts.

## Related

### Siblings
- [[knowledge/complexity/problem/logic/Satisfiability\|Satisfiability]] — arbitrary clause width
- [[knowledge/complexity/problem/graph/Independent Set\|Independent Set]] — the first reduction from 3SAT in `[AB09 §2.4]`
