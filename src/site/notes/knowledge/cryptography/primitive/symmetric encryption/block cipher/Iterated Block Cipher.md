---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/block-cipher/iterated-block-cipher/","dg-note-properties":{"aliases":["Iterated Cipher","Round Cipher","Key Expansion"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §4.2 (constructing block ciphers in practice): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents could be read; the description keeps the wording of the previous version of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]].
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §7.4.1, Definition 7.80: https://cacr.uwaterloo.ca/hac/about/chap7.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]: Import $(\mathcal K, \mathcal X)$ — the key and data block spaces of the cipher built.
> - $d$: the number of **rounds**.
> - $\hat{\mathcal K}$: the round-key space.
> - $k_1, \dots, k_d \in \hat{\mathcal K}$: the **round keys**.

> [!definition] Building Blocks
> - $\hat{\mathcal E}$: any [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|block cipher]] over $(\hat{\mathcal K}, \mathcal X)$, the **round cipher** — simple, and insecure on its own. Only its $\widehat{\mathsf{Enc}}$ and $\widehat{\mathsf{Dec}}$ are used: its keys are the round keys, not outputs of its key generation.
> - $G : \mathcal K \to \hat{\mathcal K}^d$: the **key expansion function**, a simple, not necessarily secure, [[knowledge/cryptography/special function/pseudorandom generator/Pseudorandom Generators\|PRG]].

> [!definition] Iterated Block Cipher
> - $k \leftarrow \mathsf{KeyGen}()$: (Randomized) Key-generation algorithm.
>     - **Output**: a key $k \in \mathcal K$.
>     - **Steps**:
>         1. Returns $k \xleftarrow{\$} \mathcal K$.
> - $y \leftarrow \mathsf{Enc}(k, x)$: (Deterministic) Encryption algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a data block $x \in \mathcal X$.
>     - **Output**: a data block $y \in \mathcal X$.
>     - **Steps**:
>         1. **Key expansion**: $(k_1, \dots, k_d) \leftarrow G(k)$.
>         2. **Iteration**: $y \leftarrow \widehat{\mathsf{Enc}}\big(k_d, \widehat{\mathsf{Enc}}(k_{d-1}, \dots \widehat{\mathsf{Enc}}(k_1, x) \dots)\big)$.
> - $x \leftarrow \mathsf{Dec}(k, y)$: (Deterministic) Decryption algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a data block $y \in \mathcal X$.
>     - **Output**: a data block $x \in \mathcal X$.
>     - **Steps**:
>         1. $(k_1, \dots, k_d) \leftarrow G(k)$.
>         2. $x \leftarrow \widehat{\mathsf{Dec}}\big(k_1, \widehat{\mathsf{Dec}}(k_2, \dots \widehat{\mathsf{Dec}}(k_d, y) \dots)\big)$ — the round keys in reverse order.
>
> Each application of $\widehat{\mathsf{Enc}}$ is a **round**. `[BS §4.2]` `[HAC Def 7.80]`

> [!remark] Notation in the literature
> `[HAC Def 7.80]` speaks of a **round function** repeated $r$ times, with block size $n$, key size $k$ and round keys $K_i$ derived from the key; each round function must be a bijection for a fixed round key — the round cipher $\widehat{\mathsf{Enc}}(k_i, \cdot)$ here.

## Property

### Correctness

> [!property] Correctness
> $\mathsf{Dec}(k, \mathsf{Enc}(k, x)) = x$: decryption undoes the rounds one at a time, last round first, and $\widehat{\mathsf{Dec}}(k_i, \widehat{\mathsf{Enc}}(k_i, \cdot))$ is the identity.

## Security

> [!remark] No reduction
> The paradigm comes with no security theorem in these sources: the round cipher is chosen insecure on its own `[BS §4.2]`, and the security of the cipher built is a claim about the specific design.

## Related

### Constructions
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Advanced Encryption Standard\|Advanced Encryption Standard]] — ten to fourteen rounds of SubBytes, ShiftRows, MixColumns and AddRoundKey
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] — sixteen Feistel rounds

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Feistel Network\|Feistel Network]] — one way to build the round cipher from a function that need not be invertible
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Substitution-Permutation Network\|Substitution-Permutation Network]] — the other: key mixing, invertible S-boxes, a mixing permutation
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Even-Mansour Cipher\|Even-Mansour Cipher]] — a single round: whitening keys around one public permutation
