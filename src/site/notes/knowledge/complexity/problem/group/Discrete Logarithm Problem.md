---
{"dg-publish":true,"permalink":"/knowledge/complexity/problem/group/discrete-logarithm-problem/","dg-note-properties":{"aliases":["DLP","Discrete Log Problem"]}}
---

Reference:
- `[Gal12]` — S. D. Galbraith, _Mathematics of Public Key Cryptography_ (CUP 2012), Ch. 13, _Basic Discrete Logarithm Algorithms_: Definition 13.0.1, §13.1 (exhaustive search), §13.2 (Pohlig–Hellman, Theorem 13.2.5), §13.3 (baby-step giant-step, Theorem 13.3.1), §13.4 (generic lower bound, Theorem 13.4.5, Corollary 13.4.7): https://www.math.auckland.ac.nz/~sgal018/crypto-book/ch13.pdf
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, §10.4 (the discrete logarithm function). Copy of Ch. 10: https://www.cis.upenn.edu/~sga001/classes/cis331f19/resources/bs_ch10.pdf

## Definition

> [!definition] Parameters
> - $\mathbb G$: a [[knowledge/math/algebra/structures/group/Group\|Group]], written multiplicatively.
> - $g \in \mathbb G$: the base, of order $N$; $\langle g \rangle$: the [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|cyclic subgroup]] it generates.
> - $h \in \mathbb G$: the target. $a \in \mathbb Z$: a logarithm of $h$.

> [!definition] Discrete Logarithm Relation
> ### Scope
> Instance: $(\mathbb G, g, h)$. Solution: an integer $a$.
>
> ---
> ### Condition
> The order $N$ of $g$ is typically known, $\mathbb G$ being an algebraic group over a finite field `[Gal12 §13.0]`.
>
> ---
> ### Relation
> $((\mathbb G, g, h), a) \in \mathcal R_\mathrm{DLog}$ iff
> $$g^a = h.$$
>
> `[Gal12 Def 13.0.1]`

> [!definition] Discrete Logarithm Function
> When $\mathbb G = \langle g \rangle$ has prime order $q$, the map $\mathbb Z_q \to \mathbb G$, $\alpha \mapsto g^\alpha$ — the **discrete exponentiation function** — is one-to-one and onto. Its inverse is the **discrete logarithm function** $\mathrm{Dlog}_g$: for $u \in \mathbb G$, $\mathrm{Dlog}_g(u)$ is the unique $\alpha \in \mathbb Z_q$ with
> $$u = g^\alpha.$$
> The value $g$ is the **base**. `[BS §10.4]`

## Problem

### Search Variant

> [!definition] Discrete Logarithm Problem
> Given $g, h \in \mathbb G$, find $a$, if it exists, such that $h = g^a$. `[Gal12 Def 13.0.1]`

> [!remark] No distribution
> `[Gal12 Def 13.0.1]` deliberately specifies no distribution on $g$, $h$ or $a$. Choosing one is the step from this problem to the [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|Discrete-Logarithm Assumption]].

### Decision Variant

> [!definition] Discrete Logarithm Language
> $$\mathcal L_\mathrm{DLog}(\mathbb G, g) = \{h \in \mathbb G \;:\; \exists a \in \mathbb Z,\ g^a = h\}.$$
> A solution exists iff $h \in \langle g \rangle$ `[Gal12 §13.0]`, so $\mathcal L_\mathrm{DLog}(\mathbb G, g) = \langle g \rangle$.

> [!remark] Trivial when $g$ generates the group
> For $\mathbb G = \langle g \rangle$ — the cryptographic case — every $h$ lies in $\mathcal L_\mathrm{DLog}$ and the decision variant has nothing to decide. This is why the decisional assumption of this family is about $g^{ab}$, the [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|Decisional Diffie-Hellman Assumption]], and not about $a$.

## Claim

> [!proposition] Exhaustive search — $O(N)$ group operations
> **Scope**
> - $g \in \mathbb G$: an element of order $N$.
> - $h \in \langle g \rangle$.
>
> ---
> **Property** — computing $g^a$ for $0 \leq a < N$ and comparing each with $h$ finds the logarithm with at most
> - $N - 2$ group operations;
> - $N$ comparisons.
>
> `[Gal12 §13.1]`

> [!theorem] Pohlig–Hellman — the DLP is only as hard as in the largest prime-order subgroup
> **Scope**
> - $g \in \mathbb G$: an element of order $N$, with $N$ $B$-smooth (every prime factor at most $B$).
> - $h \in \langle g \rangle$.
>
> ---
> **Property** — the Pohlig–Hellman algorithm solves the DLP with
> $$O(\log(N)^2 + B \log(N))$$
> group operations.
>
> It maps the problem into each prime-power subgroup with $\Phi_{l^e}(x) = x^{N/l^e}$ (Lemma 13.2.1) and recombines the answers by the Chinese remainder theorem. So small prime factors of $N$ add no security, and cryptography uses elements of prime order. `[Gal12 Thm 13.2.5]` — [[knowledge/cryptography/cryptanalysis/dlp/Pohlig-Hellman\|Pohlig-Hellman]]

> [!theorem] Baby-step giant-step — about $\sqrt r$ group operations and as much storage
> **Scope**
> - $g \in \mathbb G$: an element of prime order $r$.
> - $h \in \langle g \rangle$.
>
> ---
> **Property** — with $m = \lceil \sqrt r \rceil$ baby steps and giant steps, the algorithm solves the DLP in
> - $O(\sqrt r \log(r)^2)$ bit operations;
> - $O(\sqrt r \log(r))$ bits of storage.
>
> `[Gal12 Thm 13.3.1]` — [[knowledge/cryptography/cryptanalysis/dlp/Baby-Step Giant-Step\|Baby-Step Giant-Step]]

> [!theorem] Generic lower bound — no generic algorithm beats $\sqrt r$
> **Scope**
> - $\mathbb G$: a cyclic group of prime order $r$, accessed only through a group oracle (Shoup's or Maurer's generic model).
> - $m$: the number of oracle queries.
>
> ---
> **Property** — a generic algorithm succeeds with probability at most
> $$\frac{(m + 2)^2}{2r},$$
> so noticeable success needs $\Omega\big(\sqrt{r / \log(r)^c}\big)$ queries.
>
> `[Gal12 Thm 13.4.5, Cor 13.4.7]`; Nechaev showed $\Omega(\sqrt r)$ time and space, Shoup $\Omega(\sqrt r)$ time `[Gal12 §13.4]`. Baby-step giant-step and [[knowledge/cryptography/cryptanalysis/dlp/DLP Collision Algorithm\|collision methods]] meet it; group-specific methods such as [[knowledge/cryptography/cryptanalysis/dlp/Index Calculus\|Index Calculus]] in finite fields can beat it, which is why elliptic-curve groups are used.

## Related

### Instantiations
- [[knowledge/complexity/problem/group/Elliptic Curve DLP\|Elliptic Curve DLP]] — in the group of points of an elliptic curve
- [[knowledge/complexity/problem/group/Hyperelliptic Curve DLP\|Hyperelliptic Curve DLP]] — in the Jacobian of a hyperelliptic curve

### Constructions
- [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|Discrete-Logarithm Assumption]] — this problem with a distribution: the average-case hardness claim
- [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|Computational Diffie-Hellman Assumption]], [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|Decisional Diffie-Hellman Assumption]] — the problems about $g^{ab}$, no harder than this one

### Properties
- [[knowledge/cryptography/cryptanalysis/dlp/Baby-Step Giant-Step\|Baby-Step Giant-Step]], [[knowledge/cryptography/cryptanalysis/dlp/Pohlig-Hellman\|Pohlig-Hellman]], [[knowledge/cryptography/cryptanalysis/dlp/DLP Collision Algorithm\|DLP Collision Algorithm]], [[knowledge/cryptography/cryptanalysis/dlp/Index Calculus\|Index Calculus]] — the algorithms of the Claim (`cryptography/cryptanalysis/dlp/`)
