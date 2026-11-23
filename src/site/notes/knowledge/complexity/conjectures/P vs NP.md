---
{"dg-publish":true,"permalink":"/knowledge/complexity/conjectures/p-vs-np/","dg-note-properties":{"aliases":["P versus NP","P ≠ NP"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.1.1: Relation between NP and P; Section 2.2: Reducibility and NP-completeness, Theorem 2.8, p. 43; Chapter 3: Diagonalization, Section 3.4: Oracle Machines and the Limits of Diagonalization.
- `[RR97]` — A. A. Razborov, S. Rudich, _Natural proofs_, J. Comput. System Sci. 55 (1997), 24–35 — the original paper; not read.
- `[AW09]` — S. Aaronson, A. Wigderson, _Algebrization: a new barrier in complexity theory_, ACM Trans. Comput. Theory 1 (2009) — the original paper; not read.

# P vs NP

The most famous open problem in computer science: does every polynomially-verifiable language admit a polynomial-time decision procedure?

> [!conjecture] P ≠ NP
> There is a language $L \in$ [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]] with $L \notin$ [[knowledge/complexity/complexity class/class/time/Class P\|Class P]].

## Equivalent Formulations

> [!proposition] One NP-complete problem is enough
> **Scope**
> - [[knowledge/complexity/problem/logic/Satisfiability\|SAT]], or any NP-complete language.
>
> ---
> **Property**
> $\mathsf P = \mathsf{NP} \iff \mathsf{SAT} \in \mathsf P \iff$ some NP-complete language is in $\mathsf P$ $\iff$ every NP-complete language is in $\mathsf P$.
>
> `[AB09 Thm 2.8]`, by the [[knowledge/complexity/theorem/Cook-Levin Theorem\|Cook-Levin Theorem]] and [[knowledge/complexity/complexity class/operator/Hardness and Completeness#Property\|Hardness and Completeness#Property]].

## What's Known

- **Hierarchy theorems:** $\mathsf P \subsetneq \mathsf{EXP}$ unconditionally ([[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]]), so $\mathsf P \neq \mathsf{NP}$ or $\mathsf{NP} \neq \mathsf{EXP}$.
- **Relativization barrier:** there are oracles $A$, $B$ with $\mathsf P^A = \mathsf{NP}^A$ and $\mathsf P^B \neq \mathsf{NP}^B$ ([[knowledge/complexity/theorem/Baker-Gill-Solovay Theorem\|Baker-Gill-Solovay Theorem]], `[AB09 §3.4]`), so relativizing techniques cannot resolve the question.
- **Natural proofs barrier:** "natural" combinatorial circuit lower bounds cannot prove $\mathsf{NP} \not\subseteq \mathsf{P_{/poly}}$, assuming pseudorandom functions exist `[RR97]`.
- **Algebrization barrier:** an even broader class of techniques, including the arithmetization behind $\mathsf{IP} = \mathsf{PSPACE}$, is ruled out `[AW09]`.

These barriers tell us that resolving P vs NP requires fundamentally new proof techniques.

## Consequences of P = NP

- $\mathsf{NP} = \mathsf{coNP}$ ([[knowledge/complexity/complexity class/class/time/Class coNP\|Class coNP]]) and $\mathsf{EXP} = \mathsf{NEXP}$ ([[knowledge/complexity/complexity class/class/time/Class NEXP\|Class NEXP]]).
- Certificates can be found, not only shown to exist ([[knowledge/complexity/complexity class/class/time/Class NP#Property\|decision versus search]]).
- There would be no [[knowledge/complexity/complexity class/class/time/Class NP-Intermediate\|NP-intermediate]] languages.

## Stronger Conjectures

- $\mathsf{NP} \not\subseteq \mathsf{P_{/poly}}$ — even non-uniform poly-size circuits don't suffice ([[knowledge/complexity/complexity class/class/circuit/Class Ppoly\|Class Ppoly]]).
- $\mathsf{PH}$ does not collapse — the polynomial hierarchy has infinitely many levels ([[knowledge/complexity/complexity class/class/alternation/Class PH\|Class PH]]).
- [[knowledge/complexity/conjectures/Exponential Time Hypothesis\|ETH/SETH]] — quantitative refinements: SAT needs nearly $2^n$ time.

## Related

- [[knowledge/computability/computing model/turing machine/Oracle Turing Machine\|Oracle Machines]] — relativization barrier
- [[knowledge/complexity/circuit/Boolean Circuit\|Circuit Complexity]] — natural proofs barrier
- [[knowledge/complexity/conjectures/Exponential Time Hypothesis\|Exponential Time Hypothesis]] — quantitative form
- [[knowledge/complexity/conjectures/Conjectures MOC\|Conjectures MOC]]
