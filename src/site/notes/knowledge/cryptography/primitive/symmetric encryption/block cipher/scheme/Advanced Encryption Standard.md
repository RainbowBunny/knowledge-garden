---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/block-cipher/scheme/advanced-encryption-standard/","dg-note-properties":{"aliases":["AES","Rijndael","AES-128","AES-192","AES-256"]}}
---

Reference:
- `[FIPS197]` — NIST, _Advanced Encryption Standard (AES)_, FIPS 197, 2001, updated 2023 (FIPS 197-upd1): §4.2 ($\mathrm{GF}(2^8)$), §5 and Table 3 (key lengths and rounds), §5.1 (Algorithm 1, the cipher) and §5.1.1–5.1.4 (the four transformations), §5.2 (Algorithm 2, key expansion), §5.3 (Algorithm 3, the inverse cipher), Appendix B (worked example): https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197-upd1.pdf
- `[Got22]` — D. Gottesman, CMSC/Math 456 Cryptography, University of Maryland, fall 2022, lecture 8 (AES as a substitution–permutation network): https://www.cs.umd.edu/class/fall2022/cmsc456/lecture8.pdf
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §4.2.4 (case study: AES): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents could be read; the remark below keeps the wording of the previous version of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]].

## Scheme

Reference Name: $\mathsf{AES}$
Instantiates:: [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]

> [!scheme] Setting
> - $\mathrm{GF}(2^8) = \mathrm{GF}(2)[x] / (x^8 + x^4 + x^3 + x + 1)$: a byte $b_7 \dots b_0$ is the polynomial $\sum b_i x^i$ `[FIPS197 §4.2]` — a [[knowledge/math/algebra/structures/field/Field\|Field]] with $256$ elements.
> - The **state**: a $4 \times 4$ array of bytes $s_{r, c}$, filled column by column with the 16 bytes of a block, $s_{r, c} = \mathrm{in}[r + 4c]$.

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]: Import $(\mathcal K, \mathcal X)$, with $\mathcal X = \{0, 1\}^{128}$ and $\mathcal K = \{0, 1\}^{32 N_k}$.
> - $N_k \in \{4, 6, 8\}$: the key length in 32-bit words.
> - $N_r \in \{10, 12, 14\}$: the number of rounds, for AES-128, AES-192 and AES-256.
> - $N_b = 4$: the block length in words `[FIPS197 Table 3]`.
> - $\mathrm{Rcon}[j] = (x^{j-1}, 00, 00, 00)$: the round constants, with first bytes $01, 02, 04, 08, 10, 20, 40, 80, 1\mathrm b, 36$ `[FIPS197 §5.2]`.
> - $S : \{0, 1\}^8 \to \{0, 1\}^8$: the S-box, $S(b) = A \cdot b^{-1} \oplus 63$, the inverse in $\mathrm{GF}(2^8)$ (with $0^{-1} = 0$) followed by a fixed affine map of $\mathrm{GF}(2)^8$ `[FIPS197 §5.1.1]`.

> [!definition] Building Blocks
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Iterated Block Cipher\|Iterated Block Cipher]] — the round below repeated $N_r$ times, with round keys from the key expansion.
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Substitution-Permutation Network\|Substitution-Permutation Network]] — the shape of the round `[Got22]`:
>     - $\mathsf{AddRoundKey}$: the key mixing.
>     - $\mathsf{SubBytes}$: the substitution.
>     - $\mathsf{ShiftRows}$ and $\mathsf{MixColumns}$: the mixing, in place of the bit permutation — $\mathsf{MixColumns}$ is a linear map on each column.

> [!scheme] Advanced Encryption Standard
> - $k \leftarrow \mathsf{KeyGen}()$: (Randomized) Key-generation algorithm.
>     - **Output**: a key $k \in \{0, 1\}^{32 N_k}$ — 128, 192 or 256 bits.
>     - **Steps**:
>         1. Returns $k \xleftarrow{\$} \{0, 1\}^{32 N_k}$.
> - $s \leftarrow \mathsf{SubBytes}(s)$: (Deterministic) Byte substitution.
>     - **Input**: a state $s$.
>     - **Output**: a state.
>     - **Steps**:
>         1. Replaces each of the 16 bytes by its image under the S-box: $s_{r, c} \leftarrow S(s_{r, c})$ `[FIPS197 §5.1.1]`.
> - $s \leftarrow \mathsf{ShiftRows}(s)$: (Deterministic) Row shift.
>     - **Input**: a state $s$.
>     - **Output**: a state.
>     - **Steps**:
>         1. Rotates row $r$ left by $r$ bytes, for $r = 0, 1, 2, 3$ `[FIPS197 §5.1.2]`:
>            $$\begin{pmatrix}a_0 & a_1 & a_2 & a_3 \\ a_4 & a_5 & a_6 & a_7 \\ a_8 & a_9 & a_{10} & a_{11} \\ a_{12} & a_{13} & a_{14} & a_{15}\end{pmatrix} \mapsto \begin{pmatrix}a_0 & a_1 & a_2 & a_3 \\ a_5 & a_6 & a_7 & a_4 \\ a_{10} & a_{11} & a_8 & a_9 \\ a_{15} & a_{12} & a_{13} & a_{14}\end{pmatrix}.$$
> - $s \leftarrow \mathsf{MixColumns}(s)$: (Deterministic) Column mixing.
>     - **Input**: a state $s$.
>     - **Output**: a state.
>     - **Steps**:
>         1. Multiplies each column, over $\mathrm{GF}(2^8)$, by the invertible matrix `[FIPS197 §5.1.3]`
>            $$\begin{pmatrix}02 & 03 & 01 & 01 \\ 01 & 02 & 03 & 01 \\ 01 & 01 & 02 & 03 \\ 03 & 01 & 01 & 02\end{pmatrix}.$$
> - $s \leftarrow \mathsf{AddRoundKey}(s, w)$: (Deterministic) Round-key addition.
>     - **Input**: a state $s$ and a round key $w = (w_0, w_1, w_2, w_3)$.
>     - **Output**: a state.
>     - **Steps**:
>         1. XORs column $c$ of the state with the word $w_c$, for $c = 0, 1, 2, 3$ `[FIPS197 §5.1.4]`.
> - $(w_0, \dots, w_{4 N_r + 3}) \leftarrow \mathsf{KeyExpansion}(k)$: (Deterministic) Key expansion.
>     - **Input**: a key $k \in \{0, 1\}^{32 N_k}$.
>     - **Output**: $4(N_r + 1)$ words; round key $i$ is $(w_{4i}, \dots, w_{4i+3})$.
>     - **Steps**:
>         1. $w_0, \dots, w_{N_k - 1}$ are the words of $k$.
>         2. For $i = N_k, \dots, 4N_r + 3$: $t \leftarrow w_{i-1}$;
>             - if $i \bmod N_k = 0$: $t \leftarrow \mathsf{SubWord}(\mathsf{RotWord}(t)) \oplus \mathrm{Rcon}[i / N_k]$;
>             - else if $N_k > 6$ and $i \bmod N_k = 4$: $t \leftarrow \mathsf{SubWord}(t)$;
>             - $w_i \leftarrow w_{i - N_k} \oplus t$.
>
>     $\mathsf{RotWord}$ rotates the four bytes of a word left by one; $\mathsf{SubWord}$ applies $S$ to each byte `[FIPS197 §5.2, Alg 2]`.
> - $y \leftarrow \mathsf{Enc}(k, x)$: (Deterministic) Encryption algorithm — the cipher.
>     - **Input**: a key $k$ and a block $x \in \{0, 1\}^{128}$.
>     - **Output**: a block $y \in \{0, 1\}^{128}$.
>     - **Steps**:
>         1. $s \leftarrow x$; expand $k$; $s \leftarrow \mathsf{AddRoundKey}(s, \text{round key } 0)$.
>         2. For rounds $1, \dots, N_r - 1$: $\mathsf{SubBytes}$, $\mathsf{ShiftRows}$, $\mathsf{MixColumns}$, $\mathsf{AddRoundKey}$.
>         3. Final round $N_r$: $\mathsf{SubBytes}$, $\mathsf{ShiftRows}$, $\mathsf{AddRoundKey}$ — no $\mathsf{MixColumns}$.
>         4. Returns $y \leftarrow s$.
>
>     `[FIPS197 §5.1, Alg 1]`
> - $x \leftarrow \mathsf{Dec}(k, y)$: (Deterministic) Decryption algorithm — the inverse cipher.
>     - **Input**: a key $k$ and a block $y \in \{0, 1\}^{128}$.
>     - **Output**: a block $x \in \{0, 1\}^{128}$.
>     - **Steps**:
>         1. Applies the inverse transformations — $\mathsf{InvShiftRows}$, $\mathsf{InvSubBytes}$, $\mathsf{AddRoundKey}$, $\mathsf{InvMixColumns}$ — in reverse order, with the round keys in reverse order.
>
>     `[FIPS197 §5.3, Alg 3]`

> [!remark] Notation in the literature
> | source | form | differences |
> | --- | --- | --- |
> | `[FIPS197]` | $\mathsf{Cipher}$, $\mathsf{InvCipher}$, $\mathsf{KeyExpansion}$ | the general $N_k$; only these three configurations of Rijndael conform to the standard |
> | `[BS §4.2.4]` | the round permutation $\pi_\mathrm{AES}$ = SubBytes, ShiftRows, MixColumns | AES-128 only; its key expansion writes $w_{i, 0} \leftarrow w_{i-1, 0} \oplus g_i(w_{i-1, 3})$ with $g_i$ = rotate one byte, S-box each byte, XOR $c_i = x^{i-1}$ into the leftmost byte — $\mathsf{RotWord}$, $\mathsf{SubWord}$ and $\mathrm{Rcon}$ here |

## Property

### Correctness

> [!property] $\mathsf{AES}$ Correctness
> Each of $\mathsf{SubBytes}$, $\mathsf{ShiftRows}$, $\mathsf{MixColumns}$ and $\mathsf{AddRoundKey}$ is invertible — $S$ is a permutation, the matrix is invertible over $\mathrm{GF}(2^8)$ — and the inverse cipher applies their inverses in reverse order `[FIPS197 §5.3]`, so $\mathsf{Dec}(k, \mathsf{Enc}(k, x)) = x$.

### The S-box

> [!property] No fixed points, no opposite fixed points `[BS §4.2.4]`
> $$S(b) \neq b \quad \text{and} \quad S(b) \neq \bar b \qquad \text{for all } b \in \{0, 1\}^8,$$
> where $\bar b$ is the bitwise complement. Checked by computation over all $256$ bytes.

### Test vector

> [!example] AES-128 `[FIPS197 App B]`
> | | |
> | --- | --- |
> | key | `2b7e1516 28aed2a6 abf71588 09cf4f3c` |
> | plaintext | `3243f6a8 885a308d 313198a2 e0370734` |
> | ciphertext | `3925841d 02dc09fb dc118597 196a0b32` |
>
> An implementation written from the algorithms above reproduces it, and agrees with the PyCryptodome library on random inputs for all three key lengths.

## Related

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] — the earlier standard: 64-bit blocks, 56-bit keys, a Feistel round
- [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function\|Davies-Meyer Compression Function]] — how a block cipher becomes a hash; [[knowledge/cryptography/special function/hash function/scheme/Secure Hash Algorithm 256\|Secure Hash Algorithm 256]] uses its own cipher, SHACAL-2

### Prerequisites
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]], [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Iterated Block Cipher\|Iterated Block Cipher]], [[knowledge/math/algebra/structures/field/Field\|Field]]
