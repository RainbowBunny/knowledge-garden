---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/sponge-construction/","dg-note-properties":{"aliases":["Sponge"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§8.8.1: the sponge construction; §8.8.2: SHA3, SHAKE128 and SHAKE256).

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]: Import $(\mathcal M, \mathcal T)$, with $\mathcal M = \{0, 1\}^{\leq L}$ and $\mathcal T = \{0, 1\}^v$.
> - $n = r + c$: the state width.
> - $r$: the **rate** — a larger rate evaluates faster.
> - $c$: the **capacity** — a larger capacity gives better security bounds.
> - $L$: a bound on the message length.
> - $v > 0$: the output length.

> [!definition] Building Blocks
> - $\pi : \{0, 1\}^n \to \{0, 1\}^n$: any public permutation (universally quantified).

> [!definition] Sponge Construction
> - $z \leftarrow H(M, v)$: (Deterministic) Hash algorithm.
>     - **Input**: a message $M \in \{0, 1\}^{\leq L}$ and an output length $v > 0$.
>     - **Output**: $z \in \{0, 1\}^v$.
>     - **Steps**:
>         1. **Absorbing phase.** Pad $M$ and split it into $r$-bit blocks $m_1, \dots, m_s$. Set $h \leftarrow 0^n$. For $i = 1, \dots, s$: $h \leftarrow \pi\big(h \oplus (m_i \| 0^c)\big)$.
>         2. **Squeezing phase.** Set $z_1 \leftarrow h[0 \dots r - 1]$. For $i = 2, \dots, \lceil v / r \rceil$: $h \leftarrow \pi(h)$ and $z_i \leftarrow h[0 \dots r - 1]$.
>         3. Return $(z_1 \| \dots \| z_{\lceil v / r \rceil})[0 \dots v - 1]$.
>
> The message enters only the first $r$ bits of the state; the last $c$ bits are never read or written directly. `[BS §8.8.1]`

## Security

> [!security] Collision resistant in the ideal permutation model `[BS §8.8.1]`
> **Scope**
> - $\pi$: modeled as a random permutation $\Pi$, which $\mathcal A$ can query (the permutation analogue of the [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|Ideal Cipher Model]]).
> - $v \leq r$; $2^v$ and $2^c$ super-poly.
> - $\mathcal A$: a [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|collision finder]]; $q$ bounds its ideal-permutation queries plus the number of $r$-bit blocks in the messages it outputs.
>
> ---
> **Property**
> $$\mathsf{Adv}^{\mathsf{cr\text{-}ic}}_{H}(\mathcal A) \leq \frac{q (q - 1)}{2^v} + \frac{q (q + 1)}{2^c}.$$

## Related

### Constructions
- [[knowledge/cryptography/special function/hash function/scheme/Keccak\|Keccak]] — SHA-3 and SHAKE: the sponge on the Keccak-$f[1600]$ permutation

### Siblings
- [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle-Damgard Transform]] — iterates a compression function over the whole chaining value; nothing is hidden

### Prerequisites
- [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]], [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|Ideal Cipher Model]]
