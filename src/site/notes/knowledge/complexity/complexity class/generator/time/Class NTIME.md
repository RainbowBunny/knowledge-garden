---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/generator/time/class-ntime/","dg-note-properties":{"aliases":["NTIME","Nondeterministic Time"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 2: NP and NP completeness, Section 2.1.2: Nondeterministic Turing Machines, Definition 2.5, p. 41; Chapter 3: Diagonalization, Section 3.2: Nondeterministic Time Hierarchy Theorem, Theorem 3.2, p. 69.

## Definition

> [!definition] Parameters
> - $T : \mathbb N \to \mathbb N$: the time bound.

> [!definition] Class NTIME
> Requires:: [[knowledge/computability/computing model/turing machine/Non-deterministic Turing Machine\|Non-deterministic Turing Machine]]
>
> ---
> A [[knowledge/computability/language/Language\|Language]] $L \subseteq \{0, 1\}^*$ is in $\mathsf{NTIME}(T(n))$ iff there are a constant $c > 0$ and a nondeterministic Turing machine $M$ that runs in time $c \cdot T(n)$ on every branch, such that
> $$\forall x \in \{0, 1\}^*: x \in L \iff M(x) = 1,$$
> where $M(x) = 1$ means that some branch of $M$ on $x$ accepts. `[AB09 Def 2.5]`

## Property

> [!theorem] Nondeterministic time hierarchy — more time decides strictly more
> **Scope**
> - $f, g$ time-constructible with $f(n + 1) = o(g(n))$.
>
> ---
> **Property**
> $\mathsf{NTIME}(f(n)) \subsetneq \mathsf{NTIME}(g(n))$.
>
> [[knowledge/complexity/theorem/Nondeterministic Time Hierarchy Theorem\|Nondeterministic Time Hierarchy Theorem]], `[AB09 Thm 3.2]`

> [!proposition] Deterministic simulation — exponential cost
> **Scope**
> - $T$ time-constructible.
>
> ---
> **Property**
> $\mathsf{DTIME}(T(n)) \subseteq \mathsf{NTIME}(T(n)) \subseteq \bigcup_c \mathsf{DTIME}(2^{c\,T(n)})$.
>
> A deterministic machine can try every sequence of nondeterministic choices.

## Related

### Constructions
- [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]] — $\bigcup_c \mathsf{NTIME}(n^c)$
- [[knowledge/complexity/complexity class/class/time/Class NEXP\|Class NEXP]] — $\bigcup_c \mathsf{NTIME}(2^{n^c})$

### Siblings
- [[knowledge/complexity/complexity class/generator/time/Class DTIME\|Class DTIME]] — the deterministic version
