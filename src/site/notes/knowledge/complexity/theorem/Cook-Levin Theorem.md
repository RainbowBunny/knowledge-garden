---
{"dg-publish":true,"permalink":"/knowledge/complexity/theorem/cook-levin-theorem/","dg-note-properties":{"aliases":["Cook–Levin Theorem","SAT is NP-complete"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.3: The Cook-Levin Theorem: Computation is Local; Section 2.3.2: The Cook-Levin Theorem, Theorem 2.10, Lemma 2.11, p. 45, Example 2.12, Claim 2.13, p. 46, Lemma 2.14, p. 49; Section 2.4: The Web of Reductions, Theorems 2.15–2.17, pp. 51–53; Chapter 1, Remark 1.7, p. 18.

## Intuition

> [!intuition] Why
> It gives the first NP-complete problem, and every later NP-completeness proof is a reduction from SAT or one of its descendants. It also shows that P versus NP is exactly the question whether SAT has a fast algorithm.

## Definition

> [!theorem] Cook-Levin Theorem — SAT and 3SAT are NP-complete
> ### Scope
> - [[knowledge/complexity/problem/logic/Satisfiability\|SAT]]: the satisfiable CNF formulas.
> - [[knowledge/complexity/problem/logic/3Satisfiability\|3SAT]]: the satisfiable 3CNF formulas.
>
> ---
> ### Condition
> - Completeness is under [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]].
>
> ---
> ### Property
> $\mathsf{SAT}$ is [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|NP-complete]].
> $\mathsf{3SAT}$ is NP-complete.
>
> `[AB09 Thm 2.10]`

## Property

> [!proof] Why — computation is local
> 1. **Membership.** A satisfying assignment is a certificate, checkable in polynomial time, so $\mathsf{SAT} \in$ [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]].
> 2. **Hardness.** Let $L \in \mathsf{NP}$ with polynomial-time verifier $M$, and fix $x$. Run $M$ on $(x, u)$ as an **oblivious** machine: one whose head positions at each step depend only on the input length, not on the input. Every Turing machine can be simulated by an oblivious one with polynomial overhead `[AB09 Remark 1.7]`. The computation is a sequence of snapshots $z_1, \dots, z_T$ of constant size, and each $z_i$ is determined by $z_{i-1}$, by the snapshot at the previous visit of the work head, and by one input bit. Each such local rule is a CNF of constant size, so "$u$ makes $M$ accept $x$" becomes a CNF $\varphi_x$ of polynomial size, computable from $x$ in polynomial time, and $x \in L \iff \varphi_x \in \mathsf{SAT}$.
> 3. **3SAT.** A clause $\ell_1 \lor \cdots \lor \ell_k$ with $k > 3$ is replaced by $(\ell_1 \lor \ell_2 \lor z) \land (\neg z \lor \ell_3 \lor \cdots \lor \ell_k)$ with a fresh variable $z$, which preserves satisfiability; repeating gives $\mathsf{SAT} \leq_p \mathsf{3SAT}$ `[AB09 Lemma 2.14]`.
>
> `[AB09 §2.3]`: Lemma 2.11 is step 2; Claim 2.13, that every Boolean function on $\ell$ variables is a CNF of size at most $\ell 2^\ell$, makes each local rule a CNF.

> [!corollary] One problem decides P versus NP
> **Scope**
> - [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]].
>
> ---
> **Property**
> $\mathsf P = \mathsf{NP} \iff \mathsf{SAT} \in \mathsf P$.
>
> By [[knowledge/complexity/complexity class/operator/Hardness and Completeness#Property\|Hardness and Completeness#Property]]: an NP-complete language in $\mathsf P$ puts all of $\mathsf{NP}$ in $\mathsf P$.

## Example

> [!example] The web of reductions
> From 3SAT, NP-completeness spreads by Karp reductions `[AB09 Thms 2.15–2.17]`:
> - $\mathsf{3SAT} \leq_p$ [[knowledge/complexity/problem/graph/Independent Set\|INDSET]];
> - $\mathsf{SAT} \leq_p$ [[knowledge/complexity/problem/number/0-1 Integer Programming\|0/1 IPROG]];
> - and on to [[knowledge/complexity/problem/graph/Directed Hamiltonian Path\|Directed Hamiltonian Path]], [[knowledge/complexity/problem/graph/Three Coloring\|Three Coloring]], [[knowledge/complexity/problem/number/Subset Sum\|Subset Sum]], [[knowledge/complexity/problem/graph/Traveling Salesperson\|Traveling Salesperson]].

## Related

### Siblings
- [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]], [[knowledge/complexity/theorem/Ladner's Theorem\|Ladner's Theorem]] — the other foundational results of Arora–Barak Chapters 2–3

### Prerequisites
- [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]], [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]], [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]], [[knowledge/complexity/problem/logic/Satisfiability\|Satisfiability]]
