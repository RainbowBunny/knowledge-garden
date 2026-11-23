---
{"dg-publish":true,"permalink":"/knowledge/complexity/theorem/baker-gill-solovay-theorem/","dg-note-properties":{"aliases":["Baker–Gill–Solovay Theorem","Relativization Barrier"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 3: Diagonalization, Section 3.4: Oracle Machines and the Limits of Diagonalization, Theorem 3.7, p. 74.

## Intuition

> [!intuition] Why
> It explains part of why P versus NP is still open: the diagonalization arguments that separate time classes cannot separate P from NP, because they would work equally well relative to every oracle.

## Definition

> [!theorem] Baker-Gill-Solovay Theorem — the P versus NP question has both answers relative to oracles
> ### Scope
> - [[knowledge/complexity/complexity class/operator/Complexity Class with Oracle\|Oracle classes]] $\mathsf P^O$, $\mathsf{NP}^O$.
>
> ---
> ### Condition
> - None.
>
> ---
> ### Property
> There is an oracle $A$ with $\mathsf P^A = \mathsf{NP}^A$.
> There is an oracle $B$ with $\mathsf P^B \neq \mathsf{NP}^B$.
>
> `[AB09 Thm 3.7]`

## Property

> [!proof] Why
> - $A$ = [[knowledge/complexity/problem/machine/Exponential Computation\|EXPCOM]], the triples $\langle M, x, 1^n \rangle$ such that $M$ outputs $1$ on $x$ within $2^n$ steps. With this oracle a polynomial-time machine runs any exponential-time computation in one query, so $\mathsf{EXP} \subseteq \mathsf P^{A} \subseteq \mathsf{NP}^{A} \subseteq \mathsf{EXP}$.
> - For any $B$, $U_B = \{1^n : B \text{ contains a string of length } n\}$ is in $\mathsf{NP}^B$: guess the string and query it. $B$ is built in stages so that the $i$-th polynomial-time oracle machine, run on $1^n$ for a fresh large $n$, cannot query all $2^n$ strings of length $n$; $B$ then contains an unqueried one exactly when the machine rejects. So no machine decides $U_B$, and $U_B \notin \mathsf P^B$.
>
> `[AB09 §3.4]`

> [!remark] The relativization barrier
> A proof technique **relativizes** if it stays valid when every machine is given the same oracle. Diagonalization, as in the [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]], does. A relativizing proof of $\mathsf P \neq \mathsf{NP}$ would give $\mathsf P^A \neq \mathsf{NP}^A$, and one of $\mathsf P = \mathsf{NP}$ would give $\mathsf P^B = \mathsf{NP}^B$; both are false. So no relativizing technique settles the question. `[AB09 §3.4]`

## Related

### Siblings
- [[knowledge/complexity/conjectures/P vs NP\|P vs NP]] — the question this theorem constrains

### Prerequisites
- [[knowledge/computability/computing model/turing machine/Oracle Turing Machine\|Oracle Turing Machine]], [[knowledge/complexity/complexity class/operator/Complexity Class with Oracle\|Complexity Class with Oracle]]
