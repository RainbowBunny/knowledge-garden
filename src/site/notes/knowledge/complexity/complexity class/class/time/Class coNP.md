---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/class/time/class-co-np/","dg-note-properties":{"aliases":["coNP","Complement Nondeterministic Polynomial Time"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.6.1: coNP, Definition 2.19, p. 55, Definition 2.20 and Example 2.21, p. 56.

## Intuition

> [!intuition] Why
> coNP collects the problems whose no-instances have short proofs. Whether every unsatisfiable formula has a short proof of unsatisfiability is the NP versus coNP question.

## Definition

> [!definition] Class coNP
> Requires:: [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]], [[knowledge/complexity/complexity class/operator/Complement Class\|Complement Class]]
> 
> ---
> $$\mathsf{coNP} = \{L : \overline{L} \in \mathsf{NP}\}.$$
> `[AB09 Def 2.19]`

> [!definition] Class coNP (Universal Form)
> $L \in \mathsf{coNP}$ iff there are a polynomial $p : \mathbb N \to \mathbb N$ and a polynomial-time [[knowledge/computability/computing model/turing machine/Turing Machine\|Turing Machine]] $M$ such that
> $$\forall x \in \{0, 1\}^*: x \in L \iff \forall u \in \{0, 1\}^{p(|x|)}: M(x, u) = 1.$$
> `[AB09 Def 2.20]`

> [!warning] Not the complement of NP
> $\mathsf{coNP}$ is the class of complements of NP languages, not the set of languages outside $\mathsf{NP}$. That set is disjoint from $\mathsf{NP}$, while $\mathsf{coNP}$ and $\mathsf{NP}$ share all of $\mathsf P$.

## Property

> [!proposition] Complete problem — TAUTOLOGY
> **Scope**
> - [[knowledge/complexity/problem/logic/Tautology\|TAUTOLOGY]], the Boolean formulas true under every assignment.
>
> ---
> **Property**
> TAUTOLOGY is coNP-complete under [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Karp reductions]].
>
> `[AB09 Ex 2.21]`. $\varphi$ is a tautology iff $\neg \varphi$ is unsatisfiable, so this is the [[knowledge/complexity/theorem/Cook-Levin Theorem\|Cook-Levin Theorem]] seen through complements.

> [!proposition] Symmetric collapse
> **Scope**
> - [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]], $\mathsf{coNP}$.
>
> ---
> **Property**
> $\mathsf P \subseteq \mathsf{NP} \cap \mathsf{coNP}$.
> $\mathsf P = \mathsf{NP} \Rightarrow \mathsf{NP} = \mathsf{coNP}$.
>
> $\mathsf P$ is closed under complement. Whether $\mathsf{NP} = \mathsf{coNP}$ is open.

## Related

### Siblings
- [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]]
- [[knowledge/complexity/complexity class/class/alternation/Level Polynomial Hierarchy\|Level Polynomial Hierarchy]] — $\mathsf{coNP} = \Pi_1^p$
