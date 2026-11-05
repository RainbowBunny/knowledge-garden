---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/block-cipher/even-mansour-cipher/","dg-note-properties":{"aliases":["Even–Mansour","EX Construction","DESX","FX Construction"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §4.7.3 (the Even–Mansour block cipher and the EX construction), §4.7.4 (proofs): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents could be read; the definitions and the theorem keep the wording of the previous version of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]].
- `[KR01]` — J. Kilian, P. Rogaway, _How to Protect DES Against Exhaustive Key Search_, Journal of Cryptology 14(1), 17–35, 2001; earlier version CRYPTO '96 — abstract: https://www.cs.ucdavis.edu/~rogaway/papers/desx-abstract.html · paper: https://www.cs.ucdavis.edu/~rogaway/papers/desx.pdf

## Syntax

> [!definition] Parameters
> - $\mathcal X = \{0, 1\}^n$: the data block space.
> - $P_1, P_2 \in \mathcal X$: the two **whitening keys**, uniform over a subset $\mathcal X' \subseteq \mathcal X$.

> [!definition] Building Blocks
> - $\pi : \mathcal X \to \mathcal X$: a public permutation, with inverse $\pi^{-1}$ — for Even–Mansour.
> - $\mathcal E = (\mathsf{KeyGen}, \mathsf{Enc}, \mathsf{Dec})$: any [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|block cipher]] over $(\mathcal K, \mathcal X)$ — for EX.

> [!definition] Even–Mansour Cipher
> $\mathcal E_\mathrm{EM} = (\mathsf{KeyGen}, \mathsf{Enc}, \mathsf{Dec})$ over $(\mathcal X^2, \mathcal X)$:
> - $(P_1, P_2) \leftarrow \mathsf{KeyGen}()$: (Randomized) Key-generation algorithm.
>     - **Output**: a key $(P_1, P_2) \in \mathcal X^2$.
>     - **Steps**:
>         1. Returns $(P_1, P_2) \xleftarrow{\$} \mathcal X^2$.
> - $y \leftarrow \mathsf{Enc}((P_1, P_2), x)$: (Deterministic) Encryption algorithm.
>     - **Input**: a key $(P_1, P_2) \in \mathcal X^2$ and a data block $x \in \mathcal X$.
>     - **Output**: a data block $y \in \mathcal X$.
>     - **Steps**:
>         1. Returns $\pi(x \oplus P_1) \oplus P_2$.
> - $x \leftarrow \mathsf{Dec}((P_1, P_2), y)$: (Deterministic) Decryption algorithm.
>     - **Input**: a key $(P_1, P_2) \in \mathcal X^2$ and a data block $y \in \mathcal X$.
>     - **Output**: a data block $x \in \mathcal X$.
>     - **Steps**:
>         1. Returns $\pi^{-1}(y \oplus P_2) \oplus P_1$.
>
> `[BS §4.7.3]`

## Variant

### The EX construction

> [!definition] EX Construction
> Whitening around a block cipher instead of a public permutation: $\mathcal E_\mathrm{EX} = (\mathsf{KeyGen}_\mathrm{EX}, \mathsf{Enc}_\mathrm{EX}, \mathsf{Dec}_\mathrm{EX})$ over $(\mathcal K \times \mathcal X^2, \mathcal X)$,
> - $(k, P_1, P_2) \leftarrow \mathsf{KeyGen}_\mathrm{EX}()$: (Randomized) Key-generation algorithm.
>     - **Output**: a key $(k, P_1, P_2) \in \mathcal K \times \mathcal X^2$.
>     - **Steps**:
>         1. $k \leftarrow \mathsf{KeyGen}()$.
>         2. $(P_1, P_2) \xleftarrow{\$} \mathcal X^2$.
>         3. Returns $(k, P_1, P_2)$.
> - $y \leftarrow \mathsf{Enc}_\mathrm{EX}((k, P_1, P_2), x)$: (Deterministic) Encryption algorithm.
>     - **Input**: a key $(k, P_1, P_2) \in \mathcal K \times \mathcal X^2$ and a data block $x \in \mathcal X$.
>     - **Output**: a data block $y \in \mathcal X$.
>     - **Steps**:
>         1. Returns $\mathsf{Enc}(k, x \oplus P_1) \oplus P_2$.
> - $x \leftarrow \mathsf{Dec}_\mathrm{EX}((k, P_1, P_2), y)$: (Deterministic) Decryption algorithm.
>     - **Input**: a key $(k, P_1, P_2)$ and a data block $y \in \mathcal X$.
>     - **Output**: a data block $x \in \mathcal X$.
>     - **Steps**:
>         1. Returns $\mathsf{Dec}(k, y \oplus P_2) \oplus P_1$.
>
> `[BS §4.7.3]`. With $\mathcal E$ = [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] it is **DESX**: $\mathrm{DESX}_{k, k_1, k_2}(x) = k_2 \oplus \mathrm{DES}_k(k_1 \oplus x)$, proposed by Rivest as a cheap protection of DES against exhaustive key search `[KR01]`.

## Security

> [!security] EX against exhaustive search, in the ideal cipher model `[BS §4.7.3]`
> **Scope**
> - $\mathcal E$: a block cipher over $(\mathcal K, \mathcal X)$, modeled as an [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|ideal cipher]].
> - $P_1, P_2$: each uniform over $\mathcal X' \subseteq \mathcal X$.
> - $\mathcal A$: an adversary against $\mathcal E X$ making at most $Q_s$ standard queries and $Q_\mathrm{ic}$ ideal-cipher queries.
>
> ---
> **Property**
> $$\mathsf{Adv}^{\mathsf{prp\text{-}ic}}_{\mathcal E X}(\mathcal A) \leq \frac{2 Q_s Q_\mathrm{ic}}{|\mathcal K| \, |\mathcal X'|}.$$

> [!remark] Effective key length `[KR01]`
> For an idealized cipher $F$ with $k$-bit keys and $n$-bit blocks, $FX$ has effective key length at least $k + n - 1 - \lg m$ bits, where $m$ bounds the number of pairs $(x, FX(K, x))$ the adversary obtains. Exhaustive search on $F$ costs about $|\mathcal K|$; the whitening adds about $n$ bits.

## Related

### Constructions
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] — DESX

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Multiple Encryption\|Multiple Encryption]] — the other way to lengthen a key: encrypt two or three times
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Iterated Block Cipher\|Iterated Block Cipher]] — many rounds of keyed permutations; Even–Mansour is one round around a public one

### Prerequisites
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]], [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|Ideal Cipher Model]]
