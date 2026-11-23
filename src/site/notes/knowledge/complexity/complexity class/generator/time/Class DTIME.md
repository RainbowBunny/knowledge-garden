---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/generator/time/class-dtime/","dg-note-properties":{"aliases":["DTIME","Deterministic Time"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 1: The computational model —and why it doesn’t matter, Section 1.6: The Class P, Definition 1.12, p. 25; Chapter 3: Diagonalization, Section 3.1: Time Hierarchy Theorem, Theorem 3.1, p. 69.

## Intuition

> [!intuition] Why
> DTIME fixes a time budget exactly, which is what is needed to prove that more time gives more power. Named classes such as P are unions of these.

## Definition

> [!definition] Parameters
> - $T : \mathbb N \to \mathbb N$: the time bound.

> [!definition] Class DTIME
> Requires:: [[knowledge/computability/computing model/turing machine/Offline Turing Machine\|Offline Turing Machine]]
>
> ---
> A [[knowledge/computability/language/Language\|Language]] $L$ is in $\mathsf{DTIME}(T(n))$ iff some Turing machine decides $L$ in time $c \cdot T(n)$ for some constant $c > 0$. `[AB09 Def 1.12]`

> [!remark] Model-sensitive
> The D is for deterministic. Time is counted on the [[knowledge/computability/computing model/turing machine/Offline Turing Machine\|Offline Turing Machine]], the $k$-tape model of [[knowledge/complexity/complexity class/Complexity Class#Machine model\|Complexity Class#Machine model]]. On a single tape the same language may need up to the square of the time ([[knowledge/computability/computing model/turing machine/Multitape Turing Machine\|Multitape Turing Machine]]), so $\mathsf{DTIME}(T)$ depends on the model, while [[knowledge/complexity/complexity class/class/time/Class P\|Class P]] does not.

## Property

> [!theorem] Time hierarchy — more time decides strictly more
> **Scope**
> - $f, g$ time-constructible with $f(n) \log f(n) = o(g(n))$.
>
> ---
> **Property**
> $\mathsf{DTIME}(f(n)) \subsetneq \mathsf{DTIME}(g(n))$.
>
> [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]], `[AB09 Thm 3.1]`

## Related

### Constructions
- [[knowledge/complexity/complexity class/class/time/Class P\|Class P]] — $\bigcup_c \mathsf{DTIME}(n^c)$
- [[knowledge/complexity/complexity class/class/time/Class EXP\|Class EXP]] — $\bigcup_c \mathsf{DTIME}(2^{n^c})$

### Siblings
- [[knowledge/complexity/complexity class/generator/time/Class NTIME\|Class NTIME]] — the nondeterministic version
