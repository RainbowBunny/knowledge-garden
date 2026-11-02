---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/parallel-universal-hash-function-from-prf/","dg-note-properties":{"aliases":["Parallel UHF"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§7.2.3: a parallel UHF from a small PRF).
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/special function/hash function/Universal Hash Function\|Universal Hash Function]]: Import $(\mathcal K, \mathcal M, \mathcal T)$, with $\mathcal M = \mathcal X^{\leq \ell}$ and $\mathcal T = \mathcal Y$.
> - $\mathcal X$: the block set. $\ell$: a poly-bounded length. $\mathcal Y = \{0, 1\}^n$: the output set, of super-poly size.

> [!definition] Building Blocks
> - $F$: any [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Secure PRF\|secure PRF]] over $(\mathcal K, \{1, \dots, \ell\} \times \mathcal X, \mathcal Y)$ (universally quantified) — *small*: it takes one block and its position.

> [!definition] Parallel UHF from a Small PRF
> - $t \leftarrow F^\oplus(k, m)$: (Deterministic) Hash algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a message $m = (a_1, \dots, a_v) \in \mathcal X^{\leq \ell}$.
>     - **Output**: a digest $t \in \mathcal Y$.
>     - **Steps**: returns
>     $$F^\oplus(k, m) = F(k, (1, a_1)) \oplus F(k, (2, a_2)) \oplus \dots \oplus F(k, (v, a_v)).$$
>
> The $v$ calls to $F$ are independent, so they can run in parallel. `[BS §7.2.3]`
>
> `⚠️ CLAUDE – verify:` the book's text could not be read, and this note's source did not define $F^\oplus$; the definition above is reconstructed. The position $i$ is needed: without it, $(a, b)$ and $(b, a)$ always collide.

## Security

> [!security] A computational UHF `[BS §7.2.3]`
> **Scope**
> - $F$: a secure PRF; $|\mathcal Y|$ super-poly.
> - $\mathcal A$: a [[knowledge/cryptography/special function/hash function/Universal Hash Function#Secure Universal Hash Function\|UHF adversary]] against $F^\oplus$.
>
> ---
> **Property**
> There is a [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Secure PRF\|PRF adversary]] $\mathcal B$, an elementary wrapper around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{uhf}}_{F^\oplus}(\mathcal A) \leq \mathsf{Adv}^{\mathsf{prf}}_{F}(\mathcal B) + \frac{1}{|\mathcal Y|}.$$

> [!proof] Why, for the definition above
> Replace $F(k, \cdot)$ by a random function $f$; this costs $\mathsf{Adv}^{\mathsf{prf}}_F(\mathcal B)$. Each message gives a set of pairs $\{(i, a_i)\}$, and distinct messages give distinct sets, so some pair $(i, a)$ lies in exactly one of them. The XOR of the two digests then contains $f(i, a)$ exactly once; it is uniform and independent of the other terms, so the digests are equal with probability $1/|\mathcal Y|$.

## Related

### Siblings
- [[knowledge/cryptography/special function/hash function/Universal Hash Function from Prefix-Free PRF\|Universal Hash Function from Prefix-Free PRF]] — CBC and cascade: sequential, one PRF call per block in a chain

### Prerequisites
- [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|Pseudorandom Function]], [[knowledge/cryptography/special function/hash function/Universal Hash Function\|Universal Hash Function]]
