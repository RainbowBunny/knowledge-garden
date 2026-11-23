---
{"dg-publish":true,"permalink":"/knowledge/complexity/theorem/immerman-szelepcsenyi-theorem/","dg-note-properties":{"aliases":["Immerman–Szelepcsényi Theorem","NL = coNL"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 4: Space complexity, Section 4.3: NL Completeness; Section 4.3.2: NL = coNL.

## Intuition

> [!intuition] Why
> Nondeterministic space is closed under complement, while for time, as NP versus coNP, this is open. It shows that nondeterministic space is much better behaved than nondeterministic time.

## Definition

> [!theorem] Immerman-Szelepcsényi Theorem — nondeterministic logspace is closed under complement
> ### Scope
> - [[knowledge/complexity/complexity class/class/space/Class NL\|Class NL]] and its [[knowledge/complexity/complexity class/operator/Complement Class\|complement class]] $\mathsf{coNL}$.
>
> ---
> ### Condition
> - None.
>
> ---
> ### Property
> $$\mathsf{NL} = \mathsf{coNL}.$$
>
> `[AB09 §4.3.2]`

## Property

> [!proof] Why — count what is reachable
> [[knowledge/complexity/problem/graph/Vertex Path\|PATH]] is NL-complete, so it suffices to put $\overline{\mathsf{PATH}}$ in $\mathsf{NL}$: a read-once certificate that $t$ is **not** reachable from $s$. Let $C_i$ be the set of vertices reachable from $s$ in at most $i$ steps. A logspace verifier can check, inductively in $i$, a claimed value of $|C_i|$: given $|C_{i-1}|$, it walks through all vertices $v$ and, for each, either a path certifying $v \in C_i$ or, using the certified members of $C_{i-1}$ listed in order, a proof that $v \notin C_i$. With $|C_n|$ certified, it checks that the $|C_n|$ certified reachable vertices do not include $t$. `[AB09 §4.3.2]`

> [!corollary] Nondeterministic space classes are closed under complement
> **Scope**
> - $S$ space-constructible with $S(n) \geq \log n$.
>
> ---
> **Property**
> $\mathsf{NSPACE}(S(n)) = \mathsf{coNSPACE}(S(n))$.
>
> The same counting argument on the configuration graph of an $S(n)$-space machine ([[knowledge/complexity/complexity class/class/space/Class NPSPACE\|Class NPSPACE]]).

## Related

### Siblings
- [[knowledge/complexity/theorem/Savitch's Theorem\|Savitch's Theorem]]
- [[knowledge/complexity/complexity class/class/time/Class coNP\|Class coNP]] — whether the time analogue $\mathsf{NP} = \mathsf{coNP}$ holds is open

### Prerequisites
- [[knowledge/complexity/complexity class/class/space/Class NL\|Class NL]], [[knowledge/complexity/problem/graph/Vertex Path\|Vertex Path]], [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]]
