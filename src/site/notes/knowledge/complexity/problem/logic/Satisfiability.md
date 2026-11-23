---
{"dg-publish":true,"permalink":"/knowledge/complexity/problem/logic/satisfiability/","dg-note-properties":{"aliases":["SAT","CNF","Conjunctive Normal Form","Boolean Formula","Literal","Clause"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.3: The Cook-Levin Theorem: Computation is Local; Section 2.3.2: The Cook-Levin Theorem, Theorem 2.10, p. 45; Section 2.5: Decision Versus Search, Theorem 2.18, p. 55.
- `[Sip]` — M. Sipser, _Introduction to the Theory of Computation_ (edition not recorded), Chapter 7: Time Complexity, Section 7.4: NP-completeness.

## Definition

> [!definition] Boolean Formula
> A **Boolean formula** over the variables $u_1, \dots, u_n$ is built from the variables with the operators $\land$, $\lor$, $\neg$. An assignment $z \in \{0, 1\}^n$ **satisfies** $\varphi$ if $\varphi(z) = 1$, and $\varphi$ is **satisfiable** if some assignment satisfies it. `[AB09 §2.3]`

> [!definition] Literal, Clause, CNF
> - A **literal** is a variable $u_i$ or its negation $\neg u_i$.
> - A **clause** is an OR of literals.
> - A formula is in **conjunctive normal form** (CNF) if it is an AND of clauses, and in **$k$CNF** if every clause has at most $k$ literals.
>
> `[AB09 §2.3]`, `[Sip §7.4]`. Example: $(u_1 \lor \neg u_2 \lor u_3) \land (\neg u_1 \lor u_2)$ is a 3CNF.

> [!definition] SAT
> $$\mathsf{SAT} = \{\varphi : \varphi \text{ is a satisfiable CNF formula}\}.$$
> `[AB09 §2.3]`. `[Sip §7.4]` allows arbitrary Boolean formulas; the two versions are polynomially equivalent.

## Property

> [!theorem] Status — NP-complete
> Requires:: [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]]
> Complete for:: [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]] under [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]]
>
> ---
> $\mathsf{SAT}$ is NP-complete: the [[knowledge/complexity/theorem/Cook-Levin Theorem\|Cook-Levin Theorem]] `[AB09 Thm 2.10]`.

> [!proposition] Self-reducibility — deciding SAT finds assignments
> **Scope**
> - A polynomial-time decider for $\mathsf{SAT}$.
>
> ---
> **Property**
> There is a polynomial-time algorithm that outputs a satisfying assignment of every satisfiable CNF $\varphi$.
>
> `[AB09 Thm 2.18]`. Set $u_1 = 0$ and ask whether $\varphi|_{u_1 = 0}$ is satisfiable; if not, set $u_1 = 1$. Continue with $u_2, \dots, u_n$: $n$ queries in total.

## Example

> [!example] Satisfiable and unsatisfiable
> - $(u_1 \lor u_2) \land (\neg u_1 \lor u_2)$ is satisfied by $u_2 = 1$.
> - $u_1 \land \neg u_1$ is unsatisfiable.

## Related

### Descendants
- [[knowledge/complexity/problem/logic/3Satisfiability\|3Satisfiability]] — every clause has at most three literals; still NP-complete
- [[knowledge/complexity/problem/logic/True Quantified Boolean Formula\|True Quantified Boolean Formula]] — quantifiers over the variables; PSPACE-complete
- [[knowledge/complexity/problem/logic/Polynomial Hierarchy SAT\|Polynomial Hierarchy SAT]] — a fixed number of quantifier alternations

### Siblings
- [[knowledge/complexity/problem/logic/Circuit Satisfiability\|Circuit Satisfiability]] — the same question for circuits
- [[knowledge/complexity/problem/logic/Tautology\|Tautology]] — true under every assignment; coNP-complete
