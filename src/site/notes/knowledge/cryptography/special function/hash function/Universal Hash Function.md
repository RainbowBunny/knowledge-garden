---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/universal-hash-function/","dg-note-properties":{"aliases":["UHF"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§7.1: UHFs; §7.1.1: multi-query UHFs; §7.4: difference unpredictability, for the Carter–Wegman MAC; §8.10.4: the leftover hash lemma).
- `[Rey11]` — L. Reyzin, _Extractors and the Leftover Hash Lemma_, lecture 4 of MIT 6.889 _New Developments in Cryptography_, scribed by T. Steinke and D. Wilson, 2011: Definition 5, Theorem 6: https://cs-web.bu.edu/~reyzin/teaching/s11cs937/notes-leo-1.pdf
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]: Import $(\mathcal K, \mathcal M, \mathcal T, H)$ — the keyed form.

> [!definition] Universal Hash Function
> A **universal hash function** (UHF) is a [[knowledge/cryptography/special function/hash function/Hash Function#Keyed hash function\|keyed hash function]] $H$ over $(\mathcal K, \mathcal M, \mathcal T)$ used with a **secret** key: in its security games the key stays with the challenger and the adversary sees no digest, so it must find a collision blind. `[BS §7.1]`

## Security

### Secure Universal Hash Function

> [!definition] Parameters
> - $H$: a keyed hash function defined over $(\mathcal K, \mathcal M, \mathcal T)$.
> - $\varepsilon$: a bound, $0 \leq \varepsilon \leq 1$.

> [!definition] Secure Universal Hash Function
> ### Scope
> A keyed hash function $H$ defined over $(\mathcal K, \mathcal M, \mathcal T)$, against all adversaries (the bounded and statistical notions) or against efficient ones (the computational notion).
>
> ---
> ### Condition
> - **Access** — none: $\mathcal A$ sees no hash value and has no oracle; $k$ stays with the challenger.
> - **Promise** — $m_0 \neq m_1$.
> - **Quantifier** — $\forall \mathcal A$, even inefficient, for an $\varepsilon$-UHF; $\forall$ efficient $\mathcal A$ for a computational UHF.
> - **Adaptivity** — none: $\mathcal A$ commits to its messages without any information about $k$.
>
> ---
> ### Experiment
> A search game: one branch; the challenger checks the collision in the last row. `[BS §7.1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $k \xleftarrow{\$} \mathcal K$<br>keeps $k$ to itself | | |
> | 2 | | $\xleftarrow{\ m_0,\, m_1\ }$ | outputs two distinct messages $m_0, m_1 \in \mathcal M$ |
> | 3 | checks whether $H(k, m_0) = H(k, m_1)$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $H(k, m_0) = H(k, m_1)$.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{uhf}}_{H}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $H$ is an $\varepsilon$-**bounded universal hash function**, or $\varepsilon$-**UHF**, if $\mathsf{Adv}^{\mathsf{uhf}}_{H}(\mathcal A) \leq \varepsilon$ for all adversaries $\mathcal A$, even inefficient ones.
> - $H$ is a **statistical UHF** if it is an $\varepsilon$-UHF for some negligible $\varepsilon$.
> - $H$ is a **computational UHF** if $\mathsf{Adv}^{\mathsf{uhf}}_{H}(\mathcal A)$ is negligible for all efficient adversaries $\mathcal A$.
>
> It is a *search* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]]. `[BS §7.1]`

> [!remark] An alternate characterization of the $\varepsilon$-UHF property
> $\mathcal A$ learns nothing about $k$, so an unbounded $\mathcal A$ does best by outputting one fixed pair. Hence $H$ is an $\varepsilon$-UHF iff for every pair of distinct $m_0, m_1 \in \mathcal M$,
> $$\Pr_k[H(k, m_0) = H(k, m_1)] \leq \varepsilon,$$
> the probability being over the random choice of $k \in \mathcal K$ — the same shape as the DUF characterization below.

### Multi-query Universal Hash Function

> [!definition] Parameters
> - $H$: a keyed hash function defined over $(\mathcal K, \mathcal M, \mathcal T)$.
> - $Q$: a bound on the length $s$ of the list $\mathcal A$ outputs; an $\mathcal A$ that always outputs $s \leq Q$ messages is a $Q$**-query UHF adversary**.

> [!definition] Multi-query UHF
> ### Scope
> A keyed hash function $H$ defined over $(\mathcal K, \mathcal M, \mathcal T)$ and the efficient [[knowledge/cryptography/foundations/Adversary\|adversaries]].
>
> ---
> ### Condition
> - **Access** — none, as in the single-pair game.
> - **Promise** — $m_1, \dots, m_s$ are distinct, and $s \leq Q$ for a $Q$-query adversary.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — none: the whole list is output at once.
>
> ---
> ### Experiment
> A search game: one branch; the challenger checks for a collision in the last row. `[BS §7.1.1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $k \xleftarrow{\$} \mathcal K$<br>keeps $k$ to itself | | |
> | 2 | | $\xleftarrow{\ m_1, \dots, m_s\ }$ | outputs distinct messages $m_1, \dots, m_s \in \mathcal M$ |
> | 3 | checks whether $H(k, m_i) = H(k, m_j)$ for some $i \neq j$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - there are indices $i \neq j$ with $H(k, m_i) = H(k, m_j)$.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{muhf}}_{H}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $H$ is a **multi-query UHF** if $\mathsf{Adv}^{\mathsf{muhf}}_{H}(\mathcal A)$ is negligible for all efficient adversaries $\mathcal A$ `[BS §7.1.1]`.
>
> It is a *search* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

### Difference Unpredictability

> [!definition] Parameters
> - $H$: a keyed hash function defined over $(\mathcal K, \mathcal M, \mathcal T)$, where $\mathcal T = \mathbb Z_N$.
> - $\varepsilon$: a bound, $0 \leq \varepsilon \leq 1$.

> [!definition] Difference Unpredictability
> ### Scope
> A keyed hash function $H$ defined over $(\mathcal K, \mathcal M, \mathbb Z_N)$, against all adversaries (the bounded and statistical notions) or against efficient ones (the computational notion).
>
> ---
> ### Condition
> - **Access** — none: $\mathcal A$ sees no hash value and has no oracle.
> - **Promise** — $m_0 \neq m_1$.
> - **Quantifier** — $\forall \mathcal A$, even inefficient, for an $\varepsilon$-DUF; $\forall$ efficient $\mathcal A$ for a computational DUF.
> - **Adaptivity** — none: $\mathcal A$ commits without any information about $k$.
>
> ---
> ### Experiment
> A search game: one branch; the challenger checks the difference in the last row. `[BS §7.4]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $k \xleftarrow{\$} \mathcal K$<br>keeps $k$ to itself | | |
> | 2 | | $\xleftarrow{\ m_0,\, m_1,\, \delta\ }$ | outputs two distinct messages $m_0, m_1 \in \mathcal M$ and a value $\delta \in \mathcal T$ |
> | 3 | checks whether $H(k, m_1) - H(k, m_0) = \delta$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $H(k, m_1) - H(k, m_0) = \delta$.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{duf}}_{H}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $H$ is an $\varepsilon$**-bounded difference unpredictable function**, or $\varepsilon$-**DUF**, if $\mathsf{Adv}^{\mathsf{duf}}_{H}(\mathcal A) \leq \varepsilon$ for all adversaries $\mathcal A$, even inefficient ones.
> - $H$ is a **statistical DUF** if it is an $\varepsilon$-DUF for some negligible $\varepsilon$.
> - $H$ is a **computational DUF** if $\mathsf{Adv}^{\mathsf{duf}}_{H}(\mathcal A)$ is negligible for all efficient adversaries $\mathcal A$.
>
> It is a *search* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] An alternate characterization of the $\varepsilon$-DUF property
> $H$ is an $\varepsilon$-DUF iff for every pair of distinct $m_0, m_1 \in \mathcal M$ and every $\delta \in \mathcal T$,
> $$\Pr_k[H(k, m_1) - H(k, m_0) = \delta] \leq \varepsilon,$$
> the probability being over the random choice of $k \in \mathcal K$. Taking $\delta = 0$ gives the UHF condition: an $\varepsilon$-DUF is an $\varepsilon$-UHF.

## Property

### Many pairs from one

> [!lemma] Multi-query from single-pair — a computational UHF is a multi-query UHF
> **Scope**
> - $H$: a keyed hash function over $(\mathcal K, \mathcal M, \mathcal T)$.
> - $\mathcal A$: a $Q$-query UHF adversary.
>
> ---
> **Property**
> There is a UHF adversary $\mathcal B$, an elementary wrapper around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{muhf}}_{H}(\mathcal A) \leq (Q^2/2) \cdot \mathsf{Adv}^{\mathsf{uhf}}_{H}(\mathcal B).$$
> Hence a computational UHF is a multi-query UHF.
>
> `[BS §7.1.1]`

> [!proof] Why
> $\mathcal B$ runs $\mathcal A$, picks one of the at most $Q^2/2$ pairs $i < j$ of its list at random, and outputs $(m_i, m_j)$. Whenever the list contains a colliding pair, $\mathcal B$ picks it with probability at least $2/Q^2$.

### Leftover hash lemma

> [!theorem] Leftover Hash Lemma — a universal family extracts almost uniform bits
> **Scope**
> - $\mathcal H$: a family of functions $\{0, 1\}^n \to \{0, 1\}^m$ that is **universal**: for all $x \neq y$, $\Pr_{h \in \mathcal H}[h(x) = h(y)] \leq 2^{-m}$.
> - $X$: a random variable on $\{0, 1\}^n$ with min-entropy $H_\infty(X) \geq k$.
> - $\varepsilon > 0$, with $m = k - 2 \log(1/\varepsilon)$.
> - $h \xleftarrow{\$} \mathcal H$, independent of $X$; $U_m$: uniform on $\{0, 1\}^m$.
>
> ---
> **Property**
> $$\Delta\big((h, h(X)),\ (h, U_m)\big) \leq \varepsilon / 2.$$
>
> `[Rey11 Thm 6]`, stated there as: $\mathrm{Ext}(x, h) = h(x)$ is a strong $(k, \varepsilon/2)$-extractor. `[BS §8.10.4]` uses the lemma for key derivation. $\Delta$ is [[knowledge/math/probability/Statistical Distance\|statistical distance]].

> [!remark] Reading the lemma in this note's terms
> - A universal family is a $2^{-m}$-UHF with the key $h$ — the alternate characterization above with $\varepsilon = 2^{-m}$.
> - A shorter output, $m \leq k - 2 \log(1/\varepsilon)$, keeps the bound: apply the lemma with $\varepsilon' = 2^{-(k - m)/2} \leq \varepsilon$.
> - Any finite range: the proof counts collisions and uses only the size of the range, so the lemma holds for $h : \mathcal X \to \mathcal Y$ with $\log |\mathcal Y|$ in place of $m$. `⚠️ CLAUDE – verify:` `[Rey11]` states it for bit strings only.

> [!example] Matrix–vector products — a universal family over $\mathbb Z_q$
> **Scope**
> - $q$: a prime. $n, m$: positive integers.
> - $\mathcal H = \{h_\mathbf A : \mathbf r \mapsto \mathbf A \mathbf r\}_{\mathbf A \in \mathbb Z_q^{n \times m}}$: functions $\mathbb Z_q^m \to \mathbb Z_q^n$.
>
> ---
> **Property**
> $$\Pr_\mathbf A[\mathbf A \mathbf r = \mathbf A \mathbf r'] = q^{-n} \quad \text{for all } \mathbf r \neq \mathbf r' \in \mathbb Z_q^m,$$
> so $\mathcal H$ is universal with $|\mathcal Y| = q^n$.

> [!proof] Why
> $\mathbf d = \mathbf r - \mathbf r' \neq \mathbf 0$ has a nonzero coordinate, a unit since $q$ is prime. For each row $\mathbf a$ of $\mathbf A$, $\langle \mathbf a, \mathbf d \rangle$ is then uniform in $\mathbb Z_q$, so it is $0$ with probability $1/q$, independently across the $n$ rows.

## Related

### Instantiations
- [[knowledge/cryptography/special function/hash function/scheme/Polynomial Universal Hash Function\|Polynomial Universal Hash Function]] — an $(\ell/p)$-UHF over $\mathbb Z_p$; its variant $H_\mathrm{xpoly}$ is an $((\ell + 1)/p)$-DUF

### Constructions
- [[knowledge/cryptography/special function/hash function/Universal Hash Function from Prefix-Free PRF\|Universal Hash Function from Prefix-Free PRF]] — an extendable prefix-free PRF is a computational UHF; CBC and cascade are examples
- [[knowledge/cryptography/special function/hash function/Parallel Universal Hash Function from PRF\|Parallel Universal Hash Function from PRF]] — $F^\oplus$, one PRF call per block, all in parallel

### Siblings
- [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|Hash Function#Collision Resistance]] — the key is public or absent, and the adversary evaluates $H$ itself
- [[knowledge/cryptography/special function/hash function/Pairwise Independent Hash Function\|Pairwise Independent Hash Function]] — a stronger statistical condition; a pairwise independent family is universal, since $\Pr[h(x) = h(x')] = \sum_y \Pr[h(x) = y \land h(x') = y] = 2^{-k}$
