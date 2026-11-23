---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/operator/complexity-class-with-oracle/","dg-note-properties":{"aliases":["Oracle Class","Relativized Class"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 3: Diagonalization, Section 3.4: Oracle Machines and the Limits of Diagonalization, Definitions 3.4, 3.5, Example 3.6, p. 73.

## Intuition

> [!intuition] Why
> Oracles ask what a class could do if some problem were solved for free. They measure relative difficulty, build the polynomial hierarchy, and show which proof techniques cannot settle P versus NP.

## Definition

> [!definition] Parameters
> - $O \subseteq \{0, 1\}^*$: the oracle language.

> [!definition] Complexity Class with Oracle
> Requires:: [[knowledge/computability/computing model/turing machine/Oracle Turing Machine\|Oracle Turing Machine]]
>
> ---
> - $\mathsf P^O$ is the set of languages decided by a **polynomial-time** deterministic [[knowledge/computability/computing model/turing machine/Oracle Turing Machine\|Oracle Turing Machine]] with oracle access to $O$.
> - $\mathsf{NP}^O$ is the set of languages decided by a polynomial-time nondeterministic oracle Turing machine with oracle access to $O$.
>
> `[AB09 Def 3.5]`. A query is answered in one step.

## Property

> [!proposition] Oracles that do and do not help
> **Scope**
> - $O \subseteq \{0, 1\}^*$.
>
> ---
> **Property**
> $\mathsf P \subseteq \mathsf P^O$ and $\mathsf{NP} \subseteq \mathsf{NP}^O$.
> If $O \in \mathsf P$, then $\mathsf P^O = \mathsf P$.
> $\mathsf{NP} \cup \mathsf{coNP} \subseteq \mathsf P^{\mathsf{SAT}}$.
>
> A query to an oracle in $\mathsf P$ can be answered by running its algorithm. With the $\mathsf{SAT}$ oracle, one query decides any NP language after the Cook–Levin reduction, and negating the answer decides any coNP language.

> [!theorem] Relativization — both answers occur
> **Scope**
> - $\mathsf P^O$, $\mathsf{NP}^O$.
>
> ---
> **Property**
> There are oracles $A$, $B$ with $\mathsf P^A = \mathsf{NP}^A$ and $\mathsf P^B \neq \mathsf{NP}^B$.
>
> [[knowledge/complexity/theorem/Baker-Gill-Solovay Theorem\|Baker-Gill-Solovay Theorem]]

## Related

### Constructions
- [[knowledge/complexity/complexity class/class/alternation/Level Polynomial Hierarchy\|Level Polynomial Hierarchy]] — $\Sigma_{i+1}^p = \mathsf{NP}^{\Sigma_i^p}$

### Siblings
- [[knowledge/complexity/complexity class/operator/Complement Class\|Complement Class]] — the other operator that builds a class from a class
