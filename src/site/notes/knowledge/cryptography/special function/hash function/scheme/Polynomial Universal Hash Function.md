---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/scheme/polynomial-universal-hash-function/","dg-note-properties":{"aliases":["Polynomial UHF","Hpoly"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§7.2.1: the polynomial UHF $H_\mathrm{poly}$; §7.4.1: its variant $H_\mathrm{xpoly}$, a DUF, for the Carter–Wegman MAC).

## Scheme

Reference Name: $H_\mathrm{poly}$
Instantiates:: [[knowledge/cryptography/special function/hash function/Universal Hash Function\|Universal Hash Function]]

### Setting

> [!scheme] Setting
> - $\mathbb Z_p$: the integers modulo a prime $p$, a [[knowledge/math/algebra/structures/field/Field\|field]].

### Parameters

> [!definition] Parameters
> - $p$: a prime. $\ell$: a poly-bounded length parameter.
> - $\mathcal K = \mathbb Z_p$: the key space. $\mathcal M = \mathbb Z_p^{\leq \ell}$: sequences of at most $\ell$ elements. $\mathcal T = \mathbb Z_p$: the digest space.

### Algorithms

> [!scheme] Algorithms
> - $t \leftarrow H_\mathrm{poly}(k, m)$: (Deterministic) Hash algorithm.
>     - **Input**: a key $k \in \mathbb Z_p$ and a message $m = (a_1, \dots, a_v) \in \mathbb Z_p^{\leq \ell}$, $0 \leq v \leq \ell$.
>     - **Output**: a digest $t \in \mathbb Z_p$.
>     - **Steps**: returns
>     $$H_\mathrm{poly}(k, (a_1, \dots, a_v)) = k^v + a_1 k^{v-1} + a_2 k^{v-2} + \dots + a_{v-1} k + a_v.$$
>
> `[BS §7.2.1]`

## Security

### Universal hashing

> [!security] $H_\mathrm{poly}$ is an $(\ell/p)$-UHF `[BS §7.2.1]`
> **Scope**
> - $H_\mathrm{poly}$ over $(\mathbb Z_p, \mathbb Z_p^{\leq \ell}, \mathbb Z_p)$.
> - $\mathcal A$: any [[knowledge/cryptography/special function/hash function/Universal Hash Function#Secure Universal Hash Function\|UHF adversary]], even inefficient.
>
> ---
> **Property**
> $$\mathsf{Adv}^{\mathsf{uhf}}_{H_\mathrm{poly}}(\mathcal A) \leq \ell / p.$$

> [!proof] Why
> For distinct $m_0, m_1$, the difference $H_\mathrm{poly}(k, m_0) - H_\mathrm{poly}(k, m_1)$ is a polynomial in $k$ of degree at most $\ell$, and it is nonzero: if the lengths differ, the leading terms $k^{v_0}$ and $k^{v_1}$ do not cancel; if they agree, some coefficient $a_i$ differs. It has at most $\ell$ roots in $\mathbb Z_p$, so a collision has probability at most $\ell / p$ over $k$ — the [[knowledge/cryptography/special function/hash function/Universal Hash Function#Secure Universal Hash Function\|alternate characterization]].

## Variant

### $H_\mathrm{xpoly}$ — a difference unpredictable function

> [!scheme] $H_\mathrm{xpoly}$ `[BS §7.4.1]`
> $$H_\mathrm{xpoly}(k, m) = k \cdot H_\mathrm{poly}(k, m) = k^{v+1} + a_1 k^v + \dots + a_v k.$$

> [!security] $H_\mathrm{xpoly}$ is an $((\ell + 1)/p)$-DUF `[BS §7.4.1]`
> **Scope**
> - $H_\mathrm{xpoly}$ over $(\mathbb Z_p, \mathbb Z_p^{\leq \ell}, \mathbb Z_p)$.
> - $\mathcal A$: any [[knowledge/cryptography/special function/hash function/Universal Hash Function#Difference Unpredictability\|DUF adversary]], even inefficient.
>
> ---
> **Property**
> $$\mathsf{Adv}^{\mathsf{duf}}_{H_\mathrm{xpoly}}(\mathcal A) \leq (\ell + 1) / p.$$

> [!remark] Why the extra factor $k$
> $H_\mathrm{poly}$ is not a DUF: for $m_0 = (a)$ and $m_1 = (a + \delta)$, the difference $H_\mathrm{poly}(k, m_1) - H_\mathrm{poly}(k, m_0) = \delta$ for every key, so $\mathcal A$ wins with probability $1$. In $H_\mathrm{xpoly}$ the difference is $k$ times a nonzero polynomial; minus $\delta$, it stays a nonzero polynomial of degree at most $\ell + 1$, with at most $\ell + 1$ roots.

> [!remark] On $n$-bit blocks `[BS Ch. 7]`
> The same construction works in the finite field $\mathrm{GF}(2^n)$ instead of $\mathbb Z_p$, for messages made of $n$-bit blocks.

## Related

### Siblings
- [[knowledge/cryptography/special function/hash function/Pairwise Independent Hash Function\|Pairwise Independent Hash Function]] — $x \mapsto ax + b$ over $\mathrm{GF}(2^n)$: a degree-one polynomial in the message, keyed by its coefficients rather than by the evaluation point

### Prerequisites
- [[knowledge/cryptography/special function/hash function/Universal Hash Function\|Universal Hash Function]], [[knowledge/math/algebra/structures/field/Field\|Field]]
