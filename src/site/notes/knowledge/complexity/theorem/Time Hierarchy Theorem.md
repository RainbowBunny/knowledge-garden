---
{"dg-publish":true,"permalink":"/knowledge/complexity/theorem/time-hierarchy-theorem/","dg-note-properties":{"aliases":["Deterministic Time Hierarchy Theorem"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 3: Diagonalization, Section 3.1: Time Hierarchy Theorem, Theorem 3.1, p. 69; Chapter 1, Section 1.4.1: The universal Turing machine, Theorem 1.9, p. 20.
- `[Sip]` — M. Sipser, _Introduction to the Theory of Computation_ (edition not recorded), Chapter 9: Intractability, Section 9.1: Hierarchy Theorems.

## Intuition

> [!intuition] Why
> Without it no two time classes could be proved different. It shows that more time really buys more power, and gives P ≠ EXP unconditionally, one of the few class separations known.

## Definition

> [!theorem] Time Hierarchy Theorem — more time decides strictly more
> ### Scope
> - $f, g : \mathbb N \to \mathbb N$: [[knowledge/computability/computing model/Computable Function#Time-constructible Function\|time-constructible]] functions.
>
> ---
> ### Condition
> - $f(n) \log f(n) = o(g(n))$.
>
> ---
> ### Property
> $$\mathsf{DTIME}(f(n)) \subsetneq \mathsf{DTIME}(g(n)).$$
>
> `[AB09 Thm 3.1]`

## Property

> [!proof] Why — diagonalization through the universal machine
> Let $D$ be the machine that, on input $x$, runs the [[knowledge/computability/computing model/turing machine/Universal Turing Machine\|universal machine]] on $(x, x)$ for $g(|x|)$ steps and outputs the opposite answer, or $0$ if the simulation has not finished. $D$ runs in time $O(g)$. If a machine $M$ decided the same language in time $c f(n)$, then for a long enough $x$ encoding $M$, the universal machine finishes simulating $M$ on $x$ within $C c f \log f < g$ steps, and $D(x) \neq M(x)$. The $\log f$ in the hypothesis is the universal machine's $C T \log T$ overhead. `[AB09 §3.1]`

> [!remark] Sipser's form
> `[Sip §9.1]` states it as: for time-constructible $t$, some language is decidable in time $O(t(n))$ but not in time $o(t(n) / \log t(n))$. Sipser requires $t(n) \geq n \log n$ in his definition of time-constructible, while `[AB09]` requires $T(n) \geq n$ ([[knowledge/computability/computing model/Computable Function#Time-constructible Function\|Computable Function#Time-constructible Function]]); the theorems have the same content.

## Example

> [!example] Separations it gives for free
> - $\mathsf{DTIME}(n) \subsetneq \mathsf{DTIME}(n^{1.5})$, and $\mathsf{DTIME}(n^a) \subsetneq \mathsf{DTIME}(n^b)$ for $1 \leq a < b$.
> - [[knowledge/complexity/complexity class/class/time/Class P\|Class P]] $\subsetneq$ [[knowledge/complexity/complexity class/class/time/Class EXP\|Class EXP]]: $\mathsf P \subseteq \mathsf{DTIME}(2^n) \subsetneq \mathsf{DTIME}(2^{n^2}) \subseteq \mathsf{EXP}$.

## Related

### Siblings
- [[knowledge/complexity/theorem/Nondeterministic Time Hierarchy Theorem\|Nondeterministic Time Hierarchy Theorem]] — the same for $\mathsf{NTIME}$, without the log factor but with a shift $f(n + 1)$
- [[knowledge/complexity/theorem/Space Hierarchy Theorem\|Space Hierarchy Theorem]] — the same for space, without the log factor
- [[knowledge/complexity/theorem/Baker-Gill-Solovay Theorem\|Baker-Gill-Solovay Theorem]] — why diagonalization alone cannot separate $\mathsf P$ from $\mathsf{NP}$

### Prerequisites
- [[knowledge/complexity/complexity class/generator/time/Class DTIME\|Class DTIME]], [[knowledge/computability/computing model/turing machine/Universal Turing Machine\|Universal Turing Machine]]
