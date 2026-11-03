---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/block-cipher/substitution-permutation-network/","dg-note-properties":{"aliases":["SPN","SP Network","Substitution–Permutation Network"]}}
---

Reference:
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §7.4.1, Definitions 7.78 (product cipher) and 7.79 (SP network): https://cacr.uwaterloo.ca/hac/about/chap7.pdf
- `[Blo21]` — CS 555 Cryptography, Purdue University, spring 2021, week 7 slides, following Katz–Lindell §6.2.5 (Proposition 6.3): https://www.cs.purdue.edu/homes/jblocki/courses/555_Spring21/slides/Week7.pdf
- `[Got22]` — D. Gottesman, CMSC/Math 456 Cryptography, University of Maryland, fall 2022, lecture 8: https://www.cs.umd.edu/class/fall2022/cmsc456/lecture8.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]: Import $(\mathcal K, \mathcal X)$, with $\mathcal X = \{0, 1\}^n$ split into $n / b$ chunks of $b$ bits.
> - $r$: the number of rounds.
> - $k_1, \dots, k_r \in \{0, 1\}^n$: the round keys.

> [!definition] Building Blocks
> - $S_1, \dots, S_{n/b} : \{0, 1\}^b \to \{0, 1\}^b$: public **S-boxes**, each a permutation.
> - $\pi$: a public **mixing permutation** of the $n$ bit positions.
> - A key schedule that derives the round keys from the key — [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Iterated Block Cipher\|Iterated Block Cipher]].

> [!definition] Substitution–Permutation Network
> - $y \leftarrow E(k, x)$: (Deterministic) Encryption algorithm.
>     - **Input**: a key $k$ and a block $x \in \{0, 1\}^n$.
>     - **Output**: a block $y \in \{0, 1\}^n$.
>     - **Steps**:
>         1. For $i = 1, \dots, r$:
>             - **Key mixing**: $x \leftarrow x \oplus k_i$.
>             - **Substitution**: $x \leftarrow S_1(x_1) \| \cdots \| S_{n/b}(x_{n/b})$, chunk by chunk.
>             - **Permutation**: $x \leftarrow \pi(x)$, rearranging the bits.
>         2. Returns $y \leftarrow x$.
> - $x \leftarrow D(k, y)$: (Deterministic) Decryption algorithm.
>     - **Input**: a key $k$ and a block $y \in \{0, 1\}^n$.
>     - **Output**: a block $x \in \{0, 1\}^n$.
>     - **Steps**:
>         1. For $i = r, \dots, 1$: apply $\pi^{-1}$, then the inverse S-boxes $S_j^{-1}$ chunk by chunk, then XOR $k_i$.
>         2. Returns $x$.
>
> `[Blo21]`. `[HAC Def 7.79]` defines an SP network as a **product cipher** — a combination of two or more transformations meant to be more secure than each — made of stages that each involve substitution and permutation.

## Property

### A permutation

> [!proposition] An SPN is a permutation — whatever the keys and the number of rounds
> **Scope**
> - $S_1, \dots, S_{n/b}$: invertible S-boxes; $\pi$: a bit permutation.
> - $k$: any key; $r$: any number of rounds.
>
> ---
> **Property**
> $E(k, \cdot)$ is a permutation of $\{0, 1\}^n$.
>
> `[Blo21]`, citing Katz–Lindell Proposition 6.3: each step is a permutation, and so is their composition. The S-boxes must be invertible `[Got22]` — unlike the round functions of a [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Feistel Network\|Feistel Network]].

### Confusion and diffusion

> [!remark] What each step does `[Got22]`
> - The **S-boxes** give confusion: they turn their inputs into very different strings and magnify single-bit changes.
> - The **permutation** gives diffusion: it spreads the local effect of each S-box over many positions of the next round.
> - The **key mixing** is what makes it a cipher: without it, anyone could trace the permutation and S-boxes backwards to the input.
>
> Together, over several rounds, they aim at the **avalanche effect**: a change of a single input bit should give a totally different output.

## Security

> [!remark] A design paradigm, no reduction
> An SPN is a design paradigm for pseudorandom permutations `[Got22]`; its security is a claim about the specific S-boxes, permutation and number of rounds, not a theorem.

## Example

> [!example] AES
> [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Advanced Encryption Standard\|Advanced Encryption Standard]] is essentially an SPN `[Blo21]` `[Got22]`:
> - $\mathsf{AddRoundKey}$ is the key mixing;
> - $\mathsf{SubBytes}$, sixteen copies of one 8-bit S-box, is the substitution;
> - $\mathsf{ShiftRows}$ and $\mathsf{MixColumns}$ take the place of the permutation. $\mathsf{MixColumns}$ departs from the paradigm: it applies an invertible linear map to each column instead of permuting bits `[Got22]`. Its diffusion: if two input columns differ in $b > 0$ bytes, the outputs differ in at least $5 - b$ bytes `[Blo21]`.

## Related

### Constructions
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Advanced Encryption Standard\|Advanced Encryption Standard]] — the SPN of the standards

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Feistel Network\|Feistel Network]] — round functions that need not be invertible; [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] is built this way, and its round function is itself a variant of an SPN `[Got22]`
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Iterated Block Cipher\|Iterated Block Cipher]] — the general paradigm of rounds and round keys
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Even-Mansour Cipher\|Even-Mansour Cipher]] — one public permutation between two key mixings

### Prerequisites
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]
