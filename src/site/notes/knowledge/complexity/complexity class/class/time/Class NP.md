---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/class/time/class-np/","dg-note-properties":{"aliases":["NP","Nondeterministic Polynomial Time","Certificate","Witness","Verifier"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.1: The Class NP, Definition 2.1, p. 39, Example 2.3, p. 40; Section 2.1.1: Relation between NP and P, Claim 2.4, p. 41; Section 2.1.2: Nondeterministic Turing Machines, Theorem 2.6, p. 41; Section 2.2: Reducibility and NP-completeness, Theorem 2.8, p. 43; Section 2.5: Decision Versus Search, Theorem 2.18, p. 55.

## Intuition

> [!intuition] Why
> NP captures the problems whose solutions are easy to check even when they seem hard to find: a satisfying assignment, a Hamiltonian path, a factor. Thousands of practical problems have this form, and P versus NP asks whether checking is really easier than finding.

## Definition

> [!definition] Class NP
> A [[knowledge/computability/language/Language\|Language]] $L \subseteq \{0, 1\}^*$ is in $\mathsf{NP}$ iff there are a polynomial $p : \mathbb N \to \mathbb N$ and a polynomial-time [[knowledge/computability/computing model/turing machine/Turing Machine\|Turing Machine]] $M$, the **verifier** for $L$, such that
> $$\forall x \in \{0, 1\}^*: x \in L \iff \exists u \in \{0, 1\}^{p(|x|)}: M(x, u) = 1.$$
> If $x \in L$, $u \in \{0, 1\}^{p(|x|)}$ and $M(x, u) = 1$, then $u$ is a **certificate** (witness) for $x$, with respect to $L$ and $M$. `[AB09 Def 2.1]`

> [!definition] Class NP (Nondeterministic Form)
> Requires:: [[knowledge/complexity/complexity class/generator/time/Class NTIME\|Class NTIME]]
>
> ---
> $$\mathsf{NP} = \bigcup_{c \in \mathbb N} \mathsf{NTIME}(n^c).$$
> The two definitions agree `[AB09 Thm 2.6]`: an accepting sequence of nondeterministic choices is a certificate, and conversely a nondeterministic machine can guess a certificate and run the verifier.

> [!remark] Characterization by a complete problem
> $\mathsf{NP} = \{L : L \leq_p \mathsf{3SAT}\}$, by the [[knowledge/complexity/theorem/Cook-Levin Theorem\|Cook-Levin Theorem]] and because $\mathsf{NP}$ is closed under [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Karp reductions]]. This is a theorem about $\mathsf{NP}$, not its definition.

## Property

> [!proposition] Between P and EXP
> **Scope**
> - [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/class/time/Class EXP\|Class EXP]].
>
> ---
> **Property**
> $\mathsf P \subseteq \mathsf{NP} \subseteq \mathsf{EXP}$.
>
> `[AB09 Claim 2.4]`: a polynomial-time decider is a verifier that ignores $u$; and a deterministic machine can try all $2^{p(n)}$ certificates.

> [!proposition] Complete problems decide the question
> **Scope**
> - $L$ [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|NP-hard]] under Karp reductions.
>
> ---
> **Property**
> $L \in \mathsf P \Rightarrow \mathsf P = \mathsf{NP}$.
> If $L$ is NP-complete: $L \in \mathsf P \iff \mathsf P = \mathsf{NP}$.
>
> `[AB09 Thm 2.8]`

> [!theorem] Decision versus search — deciding NP gives certificates
> **Scope**
> - $L \in \mathsf{NP}$ with verifier $M$.
>
> ---
> **Condition**
> - $\mathsf P = \mathsf{NP}$.
>
> ---
> **Property**
> There is a polynomial-time Turing machine $B$ that, on every input $x \in L$, outputs a certificate for $x$ with respect to $L$ and $M$.
>
> `[AB09 Thm 2.18]`. For $\mathsf{SAT}$: fix the variables one at a time, asking the decision procedure each time whether the restricted formula is still satisfiable.

## Example

> [!example] Members of NP
> - NP-complete: [[knowledge/complexity/problem/logic/Satisfiability\|SAT]], [[knowledge/complexity/problem/logic/3Satisfiability\|3SAT]], [[knowledge/complexity/problem/graph/Independent Set\|INDSET]], [[knowledge/complexity/problem/graph/Three Coloring\|3COL]], [[knowledge/complexity/problem/number/Subset Sum\|SUBSETSUM]], [[knowledge/complexity/problem/graph/Traveling Salesperson\|TSP]], [[knowledge/complexity/problem/graph/Directed Hamiltonian Path\|dHAMPATH]], [[knowledge/complexity/problem/number/0-1 Integer Programming\|0/1 IPROG]] `[AB09 §2.4]`.
> - In $\mathsf P$: [[knowledge/complexity/problem/number/Composite Number\|COMPOSITES]], [[knowledge/complexity/problem/graph/Two Coloring\|2COL]], [[knowledge/complexity/problem/number/Linear Programming\|Linear Programming]].
> - Not known to be either: [[knowledge/complexity/problem/number/Factoring\|Factoring]], [[knowledge/complexity/problem/graph/Graph Isomorphism\|Graph Isomorphism]] ([[knowledge/complexity/complexity class/class/time/Class NP-Intermediate\|Class NP-Intermediate]]).

## Related

### Siblings
- [[knowledge/complexity/complexity class/class/time/Class coNP\|Class coNP]] — certificates for non-membership
- [[knowledge/complexity/complexity class/class/time/Class NP-Intermediate\|Class NP-Intermediate]] — neither in $\mathsf P$ nor complete, if $\mathsf P \neq \mathsf{NP}$

### Properties
- [[knowledge/complexity/theorem/Cook-Levin Theorem\|Cook-Levin Theorem]] — $\mathsf{SAT}$ is NP-complete
- [[knowledge/complexity/conjectures/P vs NP\|P vs NP]] — the open question
