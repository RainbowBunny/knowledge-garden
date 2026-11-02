---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/compression-function/davies-meyer-compression-function/","dg-note-properties":{"aliases":["Davies-Meyer","Davies–Meyer"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§8.5.2: Davies–Meyer compression functions and their variants; §8.5.3: collision resistance of Davies–Meyer in the ideal cipher model).

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/special function/compression function/Compression Functions\|Compression Functions]]: Import $(\mathcal X, \mathcal Y)$, with $\mathcal Y = \mathcal K$.
> - $\mathcal X = \{0, 1\}^n$: the chaining space, the cipher's block space. $\mathcal K$: the cipher's key space, used as the message-block space.

> [!definition] Building Blocks
> - $\mathcal E = (E, D)$: any [[knowledge/cryptography/primitive/symmetric encryption/Block Ciphers\|block cipher]] over $(\mathcal K, \mathcal X)$ (universally quantified).

> [!definition] Davies-Meyer Compression Function
> - $t \leftarrow h_\mathrm{DM}(x, y)$: (Deterministic) Compression algorithm.
>     - **Input**: a chaining value $x \in \mathcal X$ and a message block $y \in \mathcal K$.
>     - **Output**: a chaining value $t \in \mathcal X$.
>     - **Steps**: returns
>     $$h_\mathrm{DM}(x, y) = E(y, x) \oplus x.$$
>
> The message block is the cipher's **key** and the chaining value its plaintext; $h_\mathrm{DM}$ is defined over $(\mathcal X \times \mathcal K, \mathcal X)$. `[BS §8.5.2]`

## Security

> [!security] Collision resistant in the ideal cipher model `[BS §8.5.3]`
> **Scope**
> - $\mathcal E$: a block cipher over $(\mathcal K, \mathcal X)$, $|\mathcal X|$ large, modeled as an [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|ideal cipher]].
> - $\mathcal A$: a [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|collision finder]] against $h_\mathrm{DM}$ that makes at most $q$ ideal-cipher queries.
>
> ---
> **Property**
> $$\mathsf{Adv}^{\mathsf{cr\text{-}ic}}_{h_\mathrm{DM}}(\mathcal A) \leq \frac{(q + 1)(q + 2)}{|\mathcal X|}.$$

## Variant

### Where the key and the feed-forward go

> [!remark] Variants `[BS §8.5.2]`
> | name | $h(x, y)$ | collision resistant |
> | --- | --- | --- |
> | Davies–Meyer | $E(y, x) \oplus x$ | yes |
> | Matyas–Meyer–Oseas | $E(x, y) \oplus y$ | yes |
> | Miyaguchi–Preneel | $E(x, y) \oplus y \oplus x$ | yes |
> | — | $E(x \oplus y, y) \oplus y$ | yes |
> | — | $E(y, x) \oplus y$ | no |
> | — | $E(x, x \oplus y) \oplus x$ | no |
>
> "Yes" is in the ideal cipher model, as for Davies–Meyer above.

> [!attack] Why the last two fail
> Both can be inverted on any target $t$, which gives a collision with any $(x, y)$ such that $h(x, y) = t$:
> - $h(x, y) = E(y, x) \oplus y$: pick any $y'$ and set $x' = D(y', t \oplus y')$; then $h(x', y') = t$.
> - $h(x, y) = E(x, x \oplus y) \oplus x$: pick any $x'$ and set $y' = x' \oplus D(x', t \oplus x')$; then $h(x', y') = t$.
>
> In Davies–Meyer the fed-forward value $x$ is also the plaintext, so $E(y', x') \oplus x' = t$ cannot be solved for $x'$ with one call to $D$.

### Addition instead of XOR

> [!remark] $\boxplus$ in place of $\oplus$
> The final $\oplus$ can be replaced by addition: [[knowledge/cryptography/special function/hash function/scheme/SHA-256\|SHA-256]] splits the 256-bit chaining value into eight 32-bit words and adds them word by word modulo $2^{32}$.

## Related

### Constructions
- [[knowledge/cryptography/special function/hash function/scheme/SHA-256\|SHA-256]] — Davies–Meyer on the SHACAL-2 cipher, with word-wise addition, inside [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle–Damgård]]

### Siblings
- [[knowledge/cryptography/special function/compression function/scheme/Inefficient Compression Function\|Inefficient Compression Function]] — from a number-theoretic problem modulo a prime rather than from a block cipher
- [[knowledge/cryptography/special function/compression function/scheme/Two-Input Lattice Hash\|Two-Input Lattice Hash]] — from Module-SIS

### Prerequisites
- [[knowledge/cryptography/primitive/symmetric encryption/Block Ciphers\|Block Ciphers]], [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|Ideal Cipher Model]], [[knowledge/cryptography/special function/compression function/Compression Functions\|Compression Functions]]
