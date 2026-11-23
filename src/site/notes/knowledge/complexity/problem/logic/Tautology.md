---
{"dg-publish":true,"permalink":"/knowledge/complexity/problem/logic/tautology/","dg-note-properties":{"aliases":["TAUTOLOGY"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.6.1: coNP, Example 2.21, p. 56.

## Definition

> [!definition] Tautology
> $$\mathsf{TAUTOLOGY} = \{\varphi : \varphi \text{ is a Boolean formula with } \varphi(z) = 1 \text{ for every assignment } z\}.$$
> `[AB09 Ex 2.21]`

## Property

> [!theorem] Status — coNP-complete
> Requires:: [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]]
> Complete for:: [[knowledge/complexity/complexity class/class/time/Class coNP\|Class coNP]] under [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]]
>
> ---
> $\varphi \mapsto \neg \varphi$ reduces the complement of $\mathsf{SAT}$ to $\mathsf{TAUTOLOGY}$ and back, so TAUTOLOGY is coNP-complete because [[knowledge/complexity/problem/logic/Satisfiability\|SAT]] is NP-complete `[AB09 Ex 2.21]`.

## Related

### Siblings
- [[knowledge/complexity/problem/logic/Satisfiability\|Satisfiability]] — true under some assignment
