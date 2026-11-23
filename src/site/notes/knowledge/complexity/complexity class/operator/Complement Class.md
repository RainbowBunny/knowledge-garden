---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/operator/complement-class/","dg-note-properties":{"aliases":["co-Class","coC"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.6.1: coNP, Definition 2.19, p. 55.

## Definition

> [!definition] Complement Class
> ### Scope
> A [[knowledge/complexity/complexity class/Complexity Class\|Complexity Class]] $\mathsf{C}$.
> 
> ---
> ### Property
> $$\mathsf{coC} = \{L : \overline{L} \in \mathsf{C}\}, \quad \overline{L} = \{0, 1\}^* \setminus L.$$
> `[AB09 Def 2.19]`

## Property

> [!proposition] Deterministic classes are closed under complement
> **Scope**
> - $\mathsf C$ defined by deterministic machines that always halt: [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/class/time/Class EXP\|Class EXP]], [[knowledge/complexity/complexity class/class/space/Class L\|Class L]], [[knowledge/complexity/complexity class/class/space/Class PSPACE\|Class PSPACE]].
>
> ---
> **Property**
> $\mathsf{coC} = \mathsf C$.
>
> Swap the accepting and rejecting answers.

## Example

> [!example] Where it is open, and where it is a theorem
> - [[knowledge/complexity/complexity class/class/time/Class coNP\|Class coNP]]: whether $\mathsf{NP} = \mathsf{coNP}$ is open.
> - [[knowledge/complexity/complexity class/class/randomized/Class coRP\|Class coRP]]: $\mathsf{RP}$ and $\mathsf{coRP}$ differ in which side errs.
> - $\mathsf{NL} = \mathsf{coNL}$ is the Immerman–Szelepcsényi theorem ([[knowledge/complexity/complexity class/class/space/Class NL\|Class NL]]): flipping a nondeterministic answer is not trivial, but it is possible here.

## Related

### Constructions
- [[knowledge/complexity/complexity class/class/time/Class coNP\|Class coNP]], [[knowledge/complexity/complexity class/class/randomized/Class coRP\|Class coRP]]

### Siblings
- [[knowledge/complexity/complexity class/operator/Complexity Class with Oracle\|Complexity Class with Oracle]] — the other operator on classes
