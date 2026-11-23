---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/reducibility/polynomial-time-karp-reducibility/","dg-note-properties":{"aliases":["Karp Reduction","Polynomial-time Reduction","Polynomial-time Mapping Reduction"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.2: Reducibility and NP-completeness, Definition 2.7, p. 42, Theorem 2.8, p. 43.
- `[Sip]` — M. Sipser, _Introduction to the Theory of Computation_ (edition not recorded), Chapter 7: Time Complexity, Section 7.4: NP-completeness.

## Intuition

> [!intuition] Why
> A reduction from $A$ to $B$ says that $B$ is at least as hard as $A$: any algorithm for $B$ gives one for $A$. It compares problems whose absolute difficulty is unknown, which is exactly the situation inside NP.

## Definition

> [!definition] Polynomial-time Karp Reducibility
> A language $L \subseteq \{0, 1\}^*$ is **polynomial-time Karp reducible** to $L' \subseteq \{0, 1\}^*$, written $L \leq_p L'$, iff there is a polynomial-time computable function $f : \{0, 1\}^* \to \{0, 1\}^*$ such that
> $$\forall x \in \{0, 1\}^*: x \in L \iff f(x) \in L'.$$
> `[AB09 Def 2.7]`. `[Sip §7.4]` calls it a polynomial-time mapping reduction, written $\leq_{\mathrm P}$.

## Property

> [!proposition] Transitivity — reductions compose
> **Scope**
> - Languages $L$, $L'$, $L''$.
>
> ---
> **Property**
> $L \leq_p L' \land L' \leq_p L'' \Rightarrow L \leq_p L''$.
>
> `[AB09 Thm 2.8]`. If $f$, $g$ run in time $p$, $q$, then $g \circ f$ runs in time $p(n) + q(p(n))$, since $|f(x)| \leq p(|x|)$. The relation is a [[knowledge/math/set theory/order/Preorder\|Preorder]]: [[knowledge/math/property/relation/Reflexivity\|reflexive]] via the identity and [[knowledge/math/property/relation/Transitivity\|transitive]].

> [!proposition] Closure — P and NP are downward closed
> **Scope**
> - $L \leq_p L'$.
>
> ---
> **Property**
> $L' \in$ [[knowledge/complexity/complexity class/class/time/Class P\|Class P]] $\Rightarrow L \in \mathsf P$.
> $L' \in$ [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]] $\Rightarrow L \in \mathsf{NP}$.

## Example

> [!example] Reductions in the web of NP-completeness
> $\mathsf{SAT} \leq_p \mathsf{3SAT}$ ([[knowledge/complexity/theorem/Cook-Levin Theorem\|Cook-Levin Theorem]]), $\mathsf{3SAT} \leq_p \mathsf{INDSET}$ ([[knowledge/complexity/problem/graph/Independent Set\|Independent Set]]), $\mathsf{SAT} \leq_p 0/1\,\mathsf{IPROG}$ ([[knowledge/complexity/problem/number/0-1 Integer Programming\|0-1 Integer Programming]]).

## Related

### Siblings
- [[knowledge/complexity/complexity class/reducibility/Log-space Reducibility\|Log-space Reducibility]] — weaker reductions, for classes inside $\mathsf P$
- [[knowledge/complexity/complexity class/reducibility/Randomized Polynomial Reducibility\|Randomized Polynomial Reducibility]] — reductions allowed to err

### Properties
- [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]] — completeness is defined through a reducibility
