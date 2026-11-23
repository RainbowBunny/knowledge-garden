---
{"dg-publish":true,"permalink":"/knowledge/complexity/theorem/space-hierarchy-theorem/","dg-note-properties":{"aliases":["Space Hierarchy"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 4: Space complexity, Section 4.1.3: Space Hierarchy Theorem.
- `[Sip]` — M. Sipser, _Introduction to the Theory of Computation_ (edition not recorded), Chapter 9: Intractability, Section 9.1: Hierarchy Theorems, including Exponential Space Completeness.

## Intuition

> [!intuition] Why
> The same guarantee for space; it gives NL ≠ PSPACE.

## Definition

> [!theorem] Space Hierarchy Theorem — more space decides strictly more
> ### Scope
> - $f : \mathbb N \to \mathbb N$: a [[knowledge/computability/computing model/Computable Function#Space-constructible Function\|space-constructible]] function.
>
> ---
> ### Condition
> - $f(n) \geq \log n$.
>
> ---
> ### Property
> Some language is decidable in space $O(f(n))$ but not in space $o(f(n))$.
>
> `[Sip §9.1]`. `[AB09 §4.1.3]` states it as $\mathsf{SPACE}(f(n)) \subsetneq \mathsf{SPACE}(g(n))$ for space-constructible $f, g$ with $f(n) = o(g(n))$.

## Property

> [!corollary] Strict inclusions between space classes
> **Scope**
> - $f_1, f_2 : \mathbb N \to \mathbb N$ with $f_1(n) = o(f_2(n))$ and $f_2$ space-constructible.
>
> ---
> **Property**
> $$\mathsf{SPACE}(f_1(n)) \subsetneq \mathsf{SPACE}(f_2(n)).$$
> For real $0 \leq \varepsilon_1 < \varepsilon_2$: $\mathsf{SPACE}(n^{\varepsilon_1}) \subsetneq \mathsf{SPACE}(n^{\varepsilon_2})$.
>
> `[Sip §9.1]`

> [!remark] No log factor
> Unlike the [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]], a universal machine simulates a space-$s$ machine in space $O(s)$, so the gap needed is only $o$.

## Example

> [!example] Separations
> - [[knowledge/complexity/complexity class/class/space/Class NL\|Class NL]] $\subsetneq$ [[knowledge/complexity/complexity class/class/space/Class PSPACE\|Class PSPACE]] $\subsetneq \mathsf{EXPSPACE}$ `[Sip §9.1]`.
> - A natural problem outside $\mathsf{PSPACE}$: equivalence of regular expressions with exponentiation,
> $$\mathsf{EQ}_{\mathsf{REX}\uparrow} = \{\langle Q, R \rangle : Q, R \text{ are equivalent regular expressions with exponentiation}\},$$
> is $\mathsf{EXPSPACE}$-complete under polynomial-time reductions `[Sip §9.1]`, so by this theorem it is not in $\mathsf{PSPACE}$.

## Related

### Siblings
- [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]], [[knowledge/complexity/theorem/Nondeterministic Time Hierarchy Theorem\|Nondeterministic Time Hierarchy Theorem]]

### Prerequisites
- [[knowledge/complexity/complexity class/generator/space/Class SPACE\|Class SPACE]]
