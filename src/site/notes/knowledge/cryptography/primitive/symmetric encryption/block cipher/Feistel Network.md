---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/block-cipher/feistel-network/","dg-note-properties":{"aliases":["Feistel Cipher","Feistel Permutation","Luby-Rackoff Construction","Luby–Rackoff"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §4.2.1 (the Feistel permutation in DES), §4.5 (constructing block ciphers from PRFs): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents could be read; the definitions and the theorem keep the wording of the previous version of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]].
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §7.4.1, Definition 7.81: https://cacr.uwaterloo.ca/hac/about/chap7.pdf
- `[Ros]` — M. Rosulek, _The Joy of Cryptography_, Ch. 7, §7.3–7.5: Definition 7.3.1, Claim 7.3.2, Construction 7.3.3, Theorem 7.3.4, Exercises 7.5, 7.10, 7.11: https://joyofcryptography.com/prp/

## Syntax

> [!definition] Parameters
> - $\mathcal X = \{0, 1\}^n$: the half-block space.
> - $\mathcal X^2$: the block space the cipher acts on.
> - $r$: the number of rounds.
> - $(u, v)$, $(x, y) \in \mathcal X^2$: data blocks, written as left and right halves.

> [!definition] Building Blocks
> - $f, f_1, \dots, f_r : \mathcal X \to \mathcal X$: any functions (universally quantified), not necessarily invertible.
> - $F$: a [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|PRF]] over $(\mathcal K, \mathcal X, \mathcal X)$, for the keyed version.

> [!definition] Feistel Permutation and Feistel Network
> - The **Feistel permutation** of $f$ is $\pi_f : \mathcal X^2 \to \mathcal X^2$,
> $$\pi_f(x, y) = (y,\ x \oplus f(y)), \qquad \pi_f^{-1}(u, v) = (v \oplus f(u),\ u).$$
> - The **$r$-round Feistel network** is the composition $\pi_{f_r} \circ \cdots \circ \pi_{f_1}$; a block cipher built this way is a **Feistel cipher**. `[BS §4.2.1]`
>
> `[HAC Def 7.81]` writes the rounds as $L_i = R_{i-1}$, $R_i = L_{i-1} \oplus f(R_{i-1}, K_i)$ and outputs $(R_r, L_r)$, swapping the halves at the end; decryption runs the same process with $K_r, \dots, K_1$.

> [!definition] Luby–Rackoff Cipher
> The three-round Feistel network keyed by a PRF: a block cipher over $(\mathcal K^3, \mathcal X^2)$.
> - $(k_1, k_2, k_3) \leftarrow \mathsf{KeyGen}()$: (Randomized) Key-generation algorithm.
>     - **Output**: a key $(k_1, k_2, k_3) \in \mathcal K^3$.
>     - **Steps**:
>         1. Returns $(k_1, k_2, k_3) \xleftarrow{\$} \mathcal K^3$.
> - $(x, y) \leftarrow \mathsf{Enc}((k_1, k_2, k_3), (u, v))$: (Deterministic) Encryption algorithm.
>     - **Input**: a key $(k_1, k_2, k_3) \in \mathcal K^3$ and a data block $(u, v) \in \mathcal X^2$.
>     - **Output**: a data block $(x, y) \in \mathcal X^2$.
>     - **Steps**:
>         1. $w \leftarrow u \oplus F(k_1, v)$.
>         2. $x \leftarrow v \oplus F(k_2, w)$.
>         3. $y \leftarrow w \oplus F(k_3, x)$.
>         4. Returns $(x, y)$.
> - $(u, v) \leftarrow \mathsf{Dec}((k_1, k_2, k_3), (x, y))$: (Deterministic) Decryption algorithm.
>     - **Input**: a key $(k_1, k_2, k_3)$ and a data block $(x, y)$.
>     - **Output**: a data block $(u, v)$.
>     - **Steps**:
>         1. $w \leftarrow y \oplus F(k_3, x)$.
>         2. $v \leftarrow x \oplus F(k_2, w)$.
>         3. $u \leftarrow w \oplus F(k_1, v)$.
>         4. Returns $(u, v)$.
>
> `[BS §4.5]`. `[Ros Construction 7.3.3]` calls the sequence of round keys the **key schedule**.

## Property

### Always a permutation

> [!proposition] A Feistel network is a permutation, whatever its round functions — inverting it never inverts $f$
> **Scope**
> - $f_1, \dots, f_r : \mathcal X \to \mathcal X$: any functions.
>
> ---
> **Property**
> $\pi_{f_r} \circ \cdots \circ \pi_{f_1}$ is a permutation of $\mathcal X^2$, with inverse $\pi_{f_1}^{-1} \circ \cdots \circ \pi_{f_r}^{-1}$.
>
> `[Ros Claim 7.3.2]`. Each $\pi_f^{-1}$ above evaluates $f$ forwards, which is why a non-invertible $f$ suffices.

## Security

> [!security] Luby–Rackoff — three rounds of a PRF give a secure block cipher `[BS §4.5]` `[Ros Thm 7.3.4]`
> **Scope**
> - $F$: a [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Secure PRF\|secure PRF]] over $(\mathcal K, \mathcal X, \mathcal X)$, with $N = |\mathcal X| = 2^n$ super-poly.
> - $\mathcal A$: a $Q$-query [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers#Secure Block Cipher\|block cipher adversary]] against the Luby–Rackoff cipher $\mathcal E$.
>
> ---
> **Property**
> There is a PRF adversary $\mathcal B$, an elementary wrapper around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{prp}}_{\mathcal E}(\mathcal A) \leq 3 \cdot \mathsf{Adv}^{\mathsf{prf}}_{F}(\mathcal B) + \frac{Q^2}{N} + \frac{Q^2}{2N^2}.$$

> [!remark] How many rounds `[Ros §7.3–7.5]`
> | rounds | with PRF round functions |
> | --- | --- |
> | 2 | never a secure PRP `[Ros Ex 7.5]` |
> | 3 | a secure PRP, but not a strong PRP `[Ros Thm 7.3.4, Ex 7.10]` |
> | 4 | a strong PRP, with independent round keys `[Ros §7.4.1, Ex 7.11]` |

## Example

> [!example] DES
> [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] is a 16-round Feistel network on 64-bit blocks whose $i$-th round function is $F(k_i, \cdot)$, the DES round function keyed by the 48-bit round key $k_i$ `[BS §4.2.1]`.

## Related

### Constructions
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] — the Feistel cipher of the standards

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Iterated Block Cipher\|Iterated Block Cipher]] — the general paradigm; a Feistel network is one way to make its round cipher
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Substitution-Permutation Network\|Substitution-Permutation Network]] — the other way: its S-boxes must be invertible, a Feistel round function need not be
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Even-Mansour Cipher\|Even-Mansour Cipher]] — a block cipher from a public permutation instead of from functions

### Prerequisites
- [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|Pseudorandom Function]], [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]
