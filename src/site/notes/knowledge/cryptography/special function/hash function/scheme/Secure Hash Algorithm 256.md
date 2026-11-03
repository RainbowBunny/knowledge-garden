---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/scheme/secure-hash-algorithm-256/","dg-note-properties":{"aliases":["SHA-256","SHA256"]}}
---

Reference:
- `[FIPS180-4]` — NIST, _Secure Hash Standard (SHS)_, FIPS PUB 180-4, 2015: §1 (message size), §4.1.2 (functions), §4.2.2 (constants), §5.1.1 (padding), §5.3.3 (initial hash value), §6.2.2 (computation): https://csrc.nist.gov/files/pubs/fips/180-4/final/docs/fips180-4.pdf
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§8.6: case study, SHA256).
- `[Wu]` — D. J. Wu, _CS 346: Cryptography_, lecture 9, UT Austin, fall 2025: SHA-256 is Davies–Meyer inside Merkle–Damgård, with the block cipher SHACAL-2: https://www.cs.utexas.edu/~dwu4/courses/fa25/static/lecture9.pdf

## Scheme

Reference Name: $\mathsf{SHA256}$
Instantiates:: [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]

> [!scheme] Setting
> - Words: $\{0, 1\}^{32}$.
> - $+$: addition modulo $2^{32}$.
> - $\land, \lor, \oplus, \neg$: bitwise operations.
> - $\mathrm{SHR}^n(x) = x \gg n$ and $\mathrm{ROTR}^n(x) = (x \gg n) \lor (x \ll 32 - n)$.
> - For $x, y, z \in \{0, 1\}^{32}$ `[FIPS180-4 §4.1.2]`:
> $$\begin{align}
> \mathrm{Ch}(x, y, z) &= (x \land y) \oplus (\neg x \land z) \\
> \mathrm{Maj}(x, y, z) &= (x \land y) \oplus (x \land z) \oplus (y \land z) \\
> \Sigma_0(x) &= \mathrm{ROTR}^2(x) \oplus \mathrm{ROTR}^{13}(x) \oplus \mathrm{ROTR}^{22}(x) \\
> \Sigma_1(x) &= \mathrm{ROTR}^6(x) \oplus \mathrm{ROTR}^{11}(x) \oplus \mathrm{ROTR}^{25}(x) \\
> \sigma_0(x) &= \mathrm{ROTR}^7(x) \oplus \mathrm{ROTR}^{18}(x) \oplus \mathrm{SHR}^3(x) \\
> \sigma_1(x) &= \mathrm{ROTR}^{17}(x) \oplus \mathrm{ROTR}^{19}(x) \oplus \mathrm{SHR}^{10}(x)
> \end{align}$$

> [!definition] Parameters
> - Sizes `[FIPS180-4 §1]`:
>     - Message blocks: $512$ bits.
>     - Chaining values and digest: $256$ bits, eight words.
>     - Messages: fewer than $2^{64}$ bits.
> - $K_0, \dots, K_{63}$: 64 constant words, the first 32 bits of the fractional parts of the cube roots of the first 64 primes `[FIPS180-4 §4.2.2]`.
> - $IV = H^{(0)} = (\mathtt{6a09e667}, \dots, \mathtt{5be0cd19})$: eight words, from the square roots of the first eight primes `[FIPS180-4 §5.3.3]`.

> [!definition] Building Blocks
> - [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle-Damgard Transform]] — with the padding $\mathsf{Pad}$ below and $IV = H^{(0)}$.
> - [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function\|Davies-Meyer Compression Function]] — on the cipher $E$ below, with word-wise $+$ in place of $\oplus$.

> [!scheme] Secure Hash Algorithm 256
> - $\hat M \leftarrow \mathsf{Pad}(M)$: (Deterministic) Padding.
>     - **Input**: a message $M$ of $l < 2^{64}$ bits.
>     - **Output**: a padded message $\hat M$ whose length is a multiple of 512.
>     - **Steps**:
>         1. Returns $\hat M = M \| 1 \| 0^k \| \langle l \rangle_{64}$, where $k \geq 0$ is the least integer with $l + 1 + k \equiv 448 \pmod{512}$ and $\langle l \rangle_{64}$ is $l$ in 64 bits.
>
>     `[FIPS180-4 §5.1.1]`
> - $y \leftarrow E(k, x)$: (Deterministic) The block cipher SHACAL-2 `[Wu]`.
>     - **Input**: a key $k = k_0 \| \dots \| k_{15} \in \{0, 1\}^{512}$ — a message block — and a plaintext $x = x_0 \| \dots \| x_7 \in \{0, 1\}^{256}$ — a chaining value.
>     - **Output**: a ciphertext $y \in \{0, 1\}^{256}$.
>     - **Steps**:
>         1. **Key schedule** (the message schedule): $W_i = k_i$ for $0 \leq i \leq 15$, and $W_i = \sigma_1(W_{i-2}) + W_{i-7} + \sigma_0(W_{i-15}) + W_{i-16}$ for $16 \leq i \leq 63$.
>         2. $(a, b, c, d, e, f, g, h) \leftarrow (x_0, x_1, \dots, x_7)$.
>         3. For $i = 0, \dots, 63$:
>             - $T_1 \leftarrow h + \Sigma_1(e) + \mathrm{Ch}(e, f, g) + K_i + W_i$;
>             - $T_2 \leftarrow \Sigma_0(a) + \mathrm{Maj}(a, b, c)$;
>             - $(a, b, c, d, e, f, g, h) \leftarrow (T_1 + T_2,\ a,\ b,\ c,\ d + T_1,\ e,\ f,\ g)$.
>         4. Return $a \| b \| c \| d \| e \| f \| g \| h$.
>
>     `[FIPS180-4 §6.2.2]`, steps 1–3.
> - $t \leftarrow h_{256}(x, m)$: (Deterministic) Compression function — Davies–Meyer, word by word.
>     - **Input**: a chaining value $x \in \{0, 1\}^{256}$ and a message block $m \in \{0, 1\}^{512}$.
>     - **Output**: a chaining value $t \in \{0, 1\}^{256}$.
>     - **Steps**:
>         1. Returns $h_{256}(x, m) = E(m, x) + x$, the eight words added separately modulo $2^{32}$.
>
>     `[FIPS180-4 §6.2.2]`, step 4.
> - $t \leftarrow \mathsf{SHA256}(M)$: (Deterministic) Hash algorithm — Merkle–Damgård.
>     - **Input**: a message $M$ of fewer than $2^{64}$ bits.
>     - **Output**: a digest $t \in \{0, 1\}^{256}$.
>     - **Steps**:
>         1. Splits $\mathsf{Pad}(M)$ into 512-bit blocks $m_1, \dots, m_s$.
>         2. $t_0 \leftarrow H^{(0)}$.
>         3. For $i = 1, \dots, s$: $t_i \leftarrow h_{256}(t_{i-1}, m_i)$.
>         4. Returns $t_s$.

> [!remark] Notation in the literature
> `[FIPS180-4]` does not name a cipher: it writes the 64 rounds and the final addition $H^{(i)}_j = a + H^{(i-1)}_j, \dots$ as one computation on the working variables $a, \dots, h$. Reading the rounds as a block cipher keyed by the message block, and the final addition as the Davies–Meyer feed-forward, is the presentation of `[BS §8.6]` and `[Wu]`.

## Security

> [!remark] Where its collision resistance comes from
> - [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform#Security\|Merkle-Damgard Transform#Security]] turns a collision for $\mathsf{SHA256}$ into a collision for $h_{256}$; the padding encodes the length, as that proof needs.
> - [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function#Security\|Davies-Meyer Compression Function#Security]] proves Davies–Meyer collision resistant when the cipher is an ideal cipher.
>
> For SHA-256 the second step is a heuristic: SHACAL-2 is one fixed cipher, not an ideal one.

## Related

### Siblings
- [[knowledge/cryptography/special function/hash function/scheme/Message-Digest Algorithm 5\|Message-Digest Algorithm 5]] — also Merkle–Damgård, with a 128-bit digest; collisions are known
- [[knowledge/cryptography/special function/hash function/scheme/Keccak\|Keccak]] — SHA-3: a [[knowledge/cryptography/special function/hash function/Sponge Construction\|sponge]], not Merkle–Damgård

### Prerequisites
- [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle-Damgard Transform]], [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function\|Davies-Meyer Compression Function]]
