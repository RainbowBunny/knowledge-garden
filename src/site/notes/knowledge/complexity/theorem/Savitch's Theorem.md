---
{"dg-publish":true,"permalink":"/knowledge/complexity/theorem/savitch-s-theorem/","dg-note-properties":{"aliases":["Savitch Theorem","PSPACE = NPSPACE"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 4: Space complexity, Section 4.2.1: Savitch's Theorem.
- `[Sip]` — M. Sipser, _Introduction to the Theory of Computation_ (edition not recorded), Chapter 8: Space Complexity, Section 8.1: Savitch's Theorem.

## Intuition

> [!intuition] Why
> Nondeterminism seems to cost exponentially in time, but in space it costs at most a square. So for space the analogue of P versus NP is settled: PSPACE = NPSPACE.

## Definition

> [!theorem] Savitch's Theorem — nondeterminism costs at most a square in space
> ### Scope
> - $S : \mathbb N \to \mathbb N$: a [[knowledge/computability/computing model/Computable Function#Space-constructible Function\|space-constructible]] function.
>
> ---
> ### Condition
> - $S(n) \geq \log n$.
>
> ---
> ### Property
> $$\mathsf{NSPACE}(S(n)) \subseteq \mathsf{SPACE}(S(n)^2).$$
>
> `[AB09 §4.2.1]`. `[Sip §8.1]` states it for $S(n) \geq n$.

## Property

> [!proof] Why — reachability by divide and conquer
> A nondeterministic $S(n)$-space machine has at most $2^{O(S(n))}$ configurations ([[knowledge/computability/computing model/turing machine/Offline Turing Machine#Configuration\|Offline Turing Machine#Configuration]]), and it accepts $x$ iff the accepting configuration is reachable from the start configuration in the configuration graph. Decide "$v$ reaches $w$ in at most $2^i$ steps" by trying every midpoint $m$ and checking "$v$ reaches $m$ in $2^{i-1}$ steps" and "$m$ reaches $w$ in $2^{i-1}$ steps" recursively, reusing the space. The recursion has depth $O(S(n))$ and each level stores one configuration of size $O(S(n))$, so the space is $O(S(n)^2)$. `[AB09 §4.2.1]`

> [!corollary] PSPACE = NPSPACE
> **Scope**
> - [[knowledge/complexity/complexity class/class/space/Class PSPACE\|Class PSPACE]], [[knowledge/complexity/complexity class/class/space/Class NPSPACE\|Class NPSPACE]].
>
> ---
> **Property**
> $\mathsf{PSPACE} = \mathsf{NPSPACE}$.
>
> The square of a polynomial is a polynomial. For time, the analogous question is [[knowledge/complexity/conjectures/P vs NP\|P vs NP]], which is open.

## Related

### Siblings
- [[knowledge/complexity/theorem/Immerman-Szelepcsényi Theorem\|Immerman-Szelepcsényi Theorem]] — the other surprise about nondeterministic space: it is closed under complement
- [[knowledge/complexity/theorem/Space Hierarchy Theorem\|Space Hierarchy Theorem]]

### Prerequisites
- [[knowledge/complexity/complexity class/generator/space/Class SPACE\|Class SPACE]], [[knowledge/complexity/complexity class/generator/space/Class NSPACE\|Class NSPACE]], [[knowledge/complexity/problem/graph/Vertex Path\|PATH]]
