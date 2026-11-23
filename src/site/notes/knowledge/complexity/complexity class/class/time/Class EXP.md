---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/class/time/class-exp/","dg-note-properties":{"aliases":["EXP","EXPTIME","Exponential Time"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.1.1: Relation between NP and P, Claim 2.4, p. 41; Section 2.6.2: EXP and NEXP; Chapter 6: Boolean circuits, Section 6.4: P/poly and NP.

## Definition

> [!definition] Class EXP
> Requires:: [[knowledge/complexity/complexity class/generator/time/Class DTIME\|Class DTIME]]
> 
> ---
> $$\mathsf{EXP} = \bigcup_{c \geq 1} \mathsf{DTIME}(2^{n^c}).$$
> `[AB09 §2.1.1]`

## Property

> [!proposition] Strictly above P
> **Scope**
> - [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]].
>
> ---
> **Property**
> $\mathsf P \subseteq \mathsf{NP} \subseteq \mathsf{EXP}$.
> $\mathsf P \subsetneq \mathsf{EXP}$.
>
> The second line is the [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]]; so at least one of $\mathsf P \neq \mathsf{NP}$, $\mathsf{NP} \neq \mathsf{EXP}$ holds.

> [!theorem] Meyer's Theorem — EXP in P/poly collapses EXP
> **Scope**
> - [[knowledge/complexity/complexity class/class/circuit/Class Ppoly\|Class Ppoly]], $\Sigma_2^p$ from the [[knowledge/complexity/complexity class/class/alternation/Level Polynomial Hierarchy\|Level Polynomial Hierarchy]].
>
> ---
> **Property**
> $\mathsf{EXP} \subseteq \mathsf{P_{/poly}} \Rightarrow \mathsf{EXP} = \Sigma_2^p$.
>
> `[AB09 §6.4]`

## Example

> [!example] A complete problem
> [[knowledge/complexity/problem/machine/Exponential Computation\|EXPCOM]], the triples $\langle M, x, 1^n \rangle$ such that $M$ accepts $x$ within $2^n$ steps, is in $\mathsf{EXP}$, and every $L \in \mathsf{EXP}$, decided by $M$ in time $2^{|x|^c}$, reduces to it by $x \mapsto \langle M, x, 1^{|x|^c} \rangle$. It is the oracle that makes $\mathsf P$ and $\mathsf{NP}$ equal in the [[knowledge/complexity/theorem/Baker-Gill-Solovay Theorem\|Baker-Gill-Solovay Theorem]].

## Related

### Siblings
- [[knowledge/complexity/complexity class/class/time/Class NEXP\|Class NEXP]] — the nondeterministic version
