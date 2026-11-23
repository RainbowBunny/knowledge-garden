---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/class/time/class-nexp/","dg-note-properties":{"aliases":["NEXP","NEXPTIME","Nondeterministic Exponential Time"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.6.2: EXP and NEXP, Theorem 2.22, p. 57.

## Definition

> [!definition] Class NEXP
> Requires:: [[knowledge/complexity/complexity class/generator/time/Class NTIME\|Class NTIME]]
> 
> ---
> $$\mathsf{NEXP} = \bigcup_{c \geq 1} \mathsf{NTIME}(2^{n^c}).$$
> `[AB09 §2.6.2]`

## Property

> [!theorem] Padding — equalities move up
> **Scope**
> - [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]], [[knowledge/complexity/complexity class/class/time/Class EXP\|Class EXP]].
>
> ---
> **Property**
> $\mathsf P = \mathsf{NP} \Rightarrow \mathsf{EXP} = \mathsf{NEXP}$.
> Equivalently, $\mathsf{EXP} \neq \mathsf{NEXP} \Rightarrow \mathsf P \neq \mathsf{NP}$.
>
> `[AB09 Thm 2.22]`. For $L \in \mathsf{NTIME}(2^{n^c})$, the padded language $\{x\, 1^{2^{|x|^c}}\}$ is in $\mathsf{NP}$, hence in $\mathsf P$, and unpadding gives $L \in \mathsf{EXP}$.

> [!proposition] Strictly above NP
> **Scope**
> - [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]].
>
> ---
> **Property**
> $\mathsf{NP} \subsetneq \mathsf{NEXP}$, by the [[knowledge/complexity/theorem/Nondeterministic Time Hierarchy Theorem\|Nondeterministic Time Hierarchy Theorem]].

## Related

### Siblings
- [[knowledge/complexity/complexity class/class/time/Class EXP\|Class EXP]] — the deterministic version
