---
{"dg-publish":true,"permalink":"/knowledge/complexity/theorem/nondeterministic-time-hierarchy-theorem/","dg-note-properties":{"aliases":["NTIME Hierarchy Theorem"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 3: Diagonalization, Section 3.2: Nondeterministic Time Hierarchy Theorem, Theorem 3.2, p. 69.

## Intuition

> [!intuition] Why
> The same guarantee for nondeterministic time, which needs a different proof; it gives NP ≠ NEXP.

## Definition

> [!theorem] Nondeterministic Time Hierarchy Theorem — more nondeterministic time decides strictly more
> ### Scope
> - $f, g : \mathbb N \to \mathbb N$: [[knowledge/computability/computing model/Computable Function#Time-constructible Function\|time-constructible]] functions.
>
> ---
> ### Condition
> - $f(n + 1) = o(g(n))$.
>
> ---
> ### Property
> $$\mathsf{NTIME}(f(n)) \subsetneq \mathsf{NTIME}(g(n)).$$
>
> `[AB09 Thm 3.2]`

## Property

> [!remark] Why the deterministic proof does not carry over
> Flipping the answer of a nondeterministic machine requires knowing that **no** branch accepts, which a nondeterministic machine cannot check quickly. The proof instead uses **lazy diagonalization**: the diagonalizing machine disagrees with each $M_i$ only once, on one input of an exponentially long interval, and on the other inputs of the interval it copies $M_i$ one step further along. The shift to $f(n + 1)$ comes from that copying. `[AB09 §3.2]`

## Example

> [!example] $\mathsf{NP} \subsetneq \mathsf{NEXP}$
> [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]] $\subseteq \mathsf{NTIME}(2^n) \subsetneq \mathsf{NTIME}(2^{n^2}) \subseteq$ [[knowledge/complexity/complexity class/class/time/Class NEXP\|Class NEXP]].

## Related

### Siblings
- [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]] — the deterministic version
- [[knowledge/complexity/theorem/Ladner's Theorem\|Ladner's Theorem]] — also proved by lazy diagonalization

### Prerequisites
- [[knowledge/complexity/complexity class/generator/time/Class NTIME\|Class NTIME]]
