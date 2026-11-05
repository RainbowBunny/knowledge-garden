---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/block-cipher/scheme/data-encryption-standard/","dg-note-properties":{"aliases":["DES","DEA"]}}
---

Reference:
- `[FIPS46-3]` — NIST, _Data Encryption Standard (DES)_, FIPS PUB 46-3, 1999, withdrawn 19 May 2005: pp. 10–12 (enciphering and deciphering), pp. 13–15 (the cipher function $f$: $E$, the S-boxes, $P$), pp. 15–16 (TDEA), pp. 19–21 (key schedule: PC-1, shifts, PC-2): https://csrc.nist.gov/files/pubs/fips/46-3/final/docs/fips46-3.pdf
- `[SP800-67]` — NIST SP 800-67 Rev. 1, _Recommendation for the Triple Data Encryption Algorithm (TDEA) Block Cipher_, 2012 (withdrawn 2017): Foreword, §2 (the DEA, parity bits), §3.4.2 (weak and semi-weak keys): https://nvlpubs.nist.gov/nistpubs/legacy/sp/nistspecialpublication800-67r1.pdf
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §7.4 (Equations 7.4–7.5), Example 7.27: https://cacr.uwaterloo.ca/hac/about/chap7.pdf
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §4.2.1 (case study: DES): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents could be read; the remarks below keep the wording of the previous version of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]].
- `⚠️ CLAUDE – verify:` — a point I could not check against the source.

## Scheme

Reference Name: $\mathsf{DES}$
Instantiates:: [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]

> [!scheme] Setting
> - Bit strings.
> - $\oplus$: the bitwise XOR.
> - $L \| R$: a 64-bit block, split into its 32-bit halves $L$ and $R$.

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]: Import $(\mathcal K, \mathcal X)$, with $\mathcal X = \{0, 1\}^{64}$ and $\mathcal K = \{0, 1\}^{64}$: 56 key bits and 8 parity bits, one per byte, set for odd parity and not used by the algorithm `[SP800-67 §2]` `[FIPS46-3 p. 19]`.
> - $16$ rounds, with round keys $k_1, \dots, k_{16} \in \{0, 1\}^{48}$.
> - Fixed tables `[FIPS46-3]`:
>     - $\mathrm{IP}$: the initial permutation of 64 bits.
>     - $E : \{0, 1\}^{32} \to \{0, 1\}^{48}$: the expansion.
>     - $S_1, \dots, S_8 : \{0, 1\}^6 \to \{0, 1\}^4$: the eight S-boxes.
>     - $P$: the permutation of 32 bits.
>     - $\mathrm{PC\text{-}1} : \{0, 1\}^{64} \to \{0, 1\}^{56}$: permuted choice 1, the key bits that enter the key schedule.
>     - $\mathrm{PC\text{-}2} : \{0, 1\}^{56} \to \{0, 1\}^{48}$: permuted choice 2, the bits that form each round key.
>     - $1, 1, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 1$: the left-shift schedule.

> [!definition] Building Blocks
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Feistel Network\|Feistel Network]] — sixteen rounds, the $i$-th with round function $F(k_i, \cdot)$.
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Iterated Block Cipher\|Iterated Block Cipher]] — round keys from a key schedule.

> [!scheme] Data Encryption Standard
> - $k \leftarrow \mathsf{KeyGen}()$: (Randomized) Key-generation algorithm.
>     - **Output**: a key $k \in \{0, 1\}^{64}$.
>     - **Steps**:
>         1. Draw the 56 key bits uniformly: the first seven bits of each byte.
>         2. Set bits $8, 16, \dots, 64$ so that each byte has odd parity.
>         3. Returns $k$.
>
>     `[FIPS46-3 p. 19]`
> - $y \leftarrow F(k_i, R)$: (Deterministic) The cipher function $f$.
>     - **Input**: a round key $k_i \in \{0, 1\}^{48}$ and a half block $R \in \{0, 1\}^{32}$.
>     - **Output**: $y \in \{0, 1\}^{32}$.
>     - **Steps**:
>         1. $t \leftarrow E(R) \oplus k_i$, split into eight 6-bit groups $t_1 \| \cdots \| t_8$.
>         2. $s_j \leftarrow S_j(t_j)$: the first and last bits of $t_j$ select the row of the table, the middle four bits the column.
>         3. Returns $y = P(s_1 \| \cdots \| s_8)$.
>
>     `[FIPS46-3 pp. 13–15]` `[HAC Eq 7.5]`
> - $(k_1, \dots, k_{16}) \leftarrow \mathsf{KS}(k)$: (Deterministic) Key schedule.
>     - **Input**: a key $k \in \{0, 1\}^{64}$.
>     - **Output**: sixteen round keys $k_1, \dots, k_{16} \in \{0, 1\}^{48}$.
>     - **Steps**:
>         1. $C_0 \| D_0 \leftarrow \mathrm{PC\text{-}1}(k)$, two 28-bit halves.
>         2. For $i = 1, \dots, 16$: rotate $C_{i-1}$ and $D_{i-1}$ left by the $i$-th shift to get $C_i, D_i$, and set $k_i \leftarrow \mathrm{PC\text{-}2}(C_i \| D_i)$.
>
>     `[FIPS46-3 pp. 19–21]`
> - $y \leftarrow \mathsf{Enc}(k, x)$: (Deterministic) Encryption algorithm.
>     - **Input**: a key $k \in \{0, 1\}^{64}$ and a block $x \in \{0, 1\}^{64}$.
>     - **Output**: a block $y \in \{0, 1\}^{64}$.
>     - **Steps**:
>         1. $(k_1, \dots, k_{16}) \leftarrow \mathsf{KS}(k)$.
>         2. $L_0 \| R_0 \leftarrow \mathrm{IP}(x)$.
>         3. For $i = 1, \dots, 16$: $L_i \leftarrow R_{i-1}$, $R_i \leftarrow L_{i-1} \oplus F(k_i, R_{i-1})$.
>         4. Returns $y = \mathrm{IP}^{-1}(R_{16} \| L_{16})$ — the halves swapped, the **preoutput block**.
>
>     `[FIPS46-3 pp. 10–11]`
> - $x \leftarrow \mathsf{Dec}(k, y)$: (Deterministic) Decryption algorithm.
>     - **Input**: a key $k \in \{0, 1\}^{64}$ and a block $y \in \{0, 1\}^{64}$.
>     - **Output**: a block $x \in \{0, 1\}^{64}$.
>     - **Steps**:
>         1. Runs the computation of $\mathsf{Enc}$ on $y$ with the round keys in reverse order: $k_{16}$ in the first round, $k_1$ in the last.
>
>     `[FIPS46-3 p. 12]`

> [!remark] Notation in the literature
> | source | form | differences |
> | --- | --- | --- |
> | `[FIPS46-3]` | $L' = R$, $R' = L \oplus f(R, K)$; key schedule $\mathrm{KS}$ | the standard |
> | `[HAC Eq 7.4–7.5]` | $f(R, K) = P(S(E(R) \oplus K))$ | the round function in one line |
> | `[BS §4.2.1]` | round function $F(k, x)$, key expansion $G$, $\mathrm{IP}$ and $\mathrm{FP} = \mathrm{IP}^{-1}$ | each round key is 48 bits chosen from the 56-bit key, a different subset for each round |

## Property

### Correctness

> [!property] $\mathsf{DES}$ Correctness
> DES is a Feistel network, so each round is inverted by the same round with the same key; running the rounds with $k_{16}, \dots, k_1$, between $\mathrm{IP}$ and $\mathrm{IP}^{-1}$, undoes encryption `[FIPS46-3 p. 12]` ([[knowledge/cryptography/primitive/symmetric encryption/block cipher/Feistel Network#Always a permutation\|Feistel Network#Always a permutation]]).

### Weak and semi-weak keys

> [!property] Weak keys — encrypting twice is the identity
> For the four weak keys `0101010101010101`, `FEFEFEFEFEFEFEFE`, `E0E0E0E0F1F1F1F1`, `1F1F1F1F0E0E0E0E` `[SP800-67 §3.4.2]`,
> $$\mathsf{Enc}(k, \mathsf{Enc}(k, x)) = x \quad \text{for all } x.$$
> Checked by computation.

> [!property] Semi-weak key pairs — one key decrypts what the other encrypts
> `[SP800-67 §3.4.2]` lists pairs of semi-weak keys to avoid. For each pair $(k_a, k_b)$ below,
> $$\mathsf{Enc}(k_a, \mathsf{Enc}(k_b, x)) = x \quad \text{for all } x,$$
> that is, $\mathsf{Enc}(k_a, \cdot) = \mathsf{Dec}(k_b, \cdot)$:
>
> | $k_a$ | $k_b$ |
> | --- | --- |
> | `01FE01FE01FE01FE` | `FE01FE01FE01FE01` |
> | `1FE01FE00EF10EF1` | `E01FE01FF10EF10E` |
> | `01E001E001F101F1` | `E001E001F101F101` |
> | `1FFE1FFE0EFE0EFE` | `FE1FFE1FFE0EFE0E` |
> | `011F011F010E010E` | `1F011F010E010E01` |
> | `E0FEE0FEF1FEF1FE` | `FEE0FEE0FEF1FEF1` |
>
> Each pair was checked by computation with PyCryptodome. `⚠️ CLAUDE – verify:` I read `[SP800-67 §3.4.2]` through a summarizer, which counted five pairs and quoted two of the six above; check the table against the document.

### Complementation

> [!property] Complementing key and plaintext complements the ciphertext
> $$\mathsf{Enc}(\bar k, \bar x) = \overline{\mathsf{Enc}(k, x)}.$$
> Checked by computation. `⚠️ CLAUDE – verify:` none of the sources I could read states it; `[HAC §7.4]` treats DES properties in a part I could not read.

## Cryptanalysis

> [!attack] Exhaustive key search `[HAC Ex 7.27]`
> With one plaintext–ciphertext pair, exhaustive search over the 56-bit key takes $2^{55}$ decryptions on average.

> [!remark] Status
> FIPS 46-3 was withdrawn on 19 May 2005 `[FIPS46-3]`; `[SP800-67]` allows the DEA only as a component of TDEA.

> [!remark] IP and FP `[BS §4.2.1]`
> The initial and final permutations have no cryptographic significance. Bit permutations are slow in software and fast in hardware, and one theory is that they were included to slow down software implementations.

## Variant

- **Triple-DES** — E-D-E with two or three keys: [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Multiple Encryption#Triple-DES\|Multiple Encryption#Triple-DES]].
- **DESX** — whitening keys before and after DES: [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Even-Mansour Cipher#The EX construction\|Even-Mansour Cipher#The EX construction]].

## Related

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Advanced Encryption Standard\|Advanced Encryption Standard]] — the later standard: 128-bit blocks, longer keys, not a Feistel cipher
- [[knowledge/cryptography/cryptanalysis/Linear Cryptanalysis\|Linear Cryptanalysis]] — a known-plaintext attack whose cost is its data complexity

### Prerequisites
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]], [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Feistel Network\|Feistel Network]]
