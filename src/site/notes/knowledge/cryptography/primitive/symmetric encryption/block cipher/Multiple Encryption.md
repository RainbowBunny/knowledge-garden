---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/block-cipher/multiple-encryption/","dg-note-properties":{"aliases":["Double Encryption","Triple Encryption","3E Construction","Triple-DES","3DES","TDEA"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §4.2.3 (the 3E construction): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents could be read; the definitions and theorems keep the wording of the previous version of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]].
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §7.2.3: Definitions 7.31 and 7.32, Fact 7.33, Example 7.36, Note 7.37: https://cacr.uwaterloo.ca/hac/about/chap7.pdf
- `[FIPS46-3]` — NIST, _Data Encryption Standard (DES)_, FIPS PUB 46-3, 1999 (withdrawn 2005), pp. 15–16 (TDEA and its keying options): https://csrc.nist.gov/files/pubs/fips/46-3/final/docs/fips46-3.pdf
- `[BR06]` — M. Bellare, P. Rogaway, _Code-Based Game-Playing Proofs and the Security of Triple Encryption_, EUROCRYPT 2006; ePrint 2004/331, abstract: https://eprint.iacr.org/2004/331

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]]: Import $(\mathcal K, \mathcal X)$.
> - $k_1, k_2, k_3 \in \mathcal K$: independent keys.

> [!definition] Building Blocks
> - $\mathcal E = (E, D)$: any [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|block cipher]] over $(\mathcal K, \mathcal X)$ (universally quantified).

> [!definition] Double and Triple Encryption
> Block ciphers over $(\mathcal K^2, \mathcal X)$ and $(\mathcal K^3, \mathcal X)$:
> - **2E**: $E_2((k_1, k_2), x) = E(k_2, E(k_1, x))$ `[BS §4.2.3]` `[HAC Def 7.31]`.
> - **3E**: $E_3((k_1, k_2, k_3), x) = E(k_3, E(k_2, E(k_1, x)))$ `[BS §4.2.3]`.
> - **E-D-E**: $E_\mathrm{EDE}((k_1, k_2, k_3), x) = E(k_3, D(k_2, E(k_1, x)))$ `[HAC Def 7.32]`.
>
> Decryption applies the inverses in reverse order.

## Property

### Keying options of E-D-E

> [!property] E-D-E with repeated keys `[HAC Def 7.32]` `[FIPS46-3]`
> - $k_1, k_2, k_3$ independent: **three-key** triple encryption.
> - $k_3 = k_1$: **two-key** triple encryption.
> - $k_1 = k_2 = k_3$: the middle decryption cancels the first encryption, and E-D-E is single encryption — so one implementation serves both.

## Security

> [!attack] Double encryption — meet in the middle `[BS §4.2.3]` `[HAC Fact 7.33]`
> **Scope**
> - $\mathcal E$: a block cipher over $(\mathcal K, \mathcal X)$.
> - $(x_i, y_i)$, $i = 1, \dots, Q$: plaintext–ciphertext pairs under $E_2$.
>
> ---
> **Property**
> An algorithm finds a key pair $(k_1, k_2) \in \mathcal K^2$ with
> $$y_i = E_2((k_1, k_2), x_i) \quad \text{for all } i = 1, \dots, Q,$$
> in time dominated by $2Q \cdot |\mathcal K|$ evaluations of $E$ and $D$ `[BS §4.2.3]`: tabulate $E(k_1, x_1)$ for every $k_1$, then look up $D(k_2, y_1)$ for every $k_2$ and check the matches on the other pairs. For a $k$-bit key this is about $2^k$ operations and $2^k$ storage `[HAC Fact 7.33]` — for double DES, $2^{56}$ time and space instead of $2^{112}$ time `[HAC Ex 7.36]`. So 2E is no more secure than $\mathcal E$ against exhaustive search.

> [!security] Triple encryption in the ideal cipher model `[BS §4.2.3]`
> **Scope**
> - $\mathcal E$: an ideal block cipher over $(\mathcal K, \mathcal X)$.
> - $\mathcal A$: an adversary against 3E making at most $Q$ queries, standard and ideal-cipher together.
> - $L = \max(|\mathcal K| / |\mathcal X|, \log_2 |\mathcal X|)$; $C_1, C_2, C_3$: constants independent of $\mathcal A$ and $\mathcal E$.
>
> ---
> **Property**
> $$\mathsf{Adv}^{\mathsf{prp\text{-}ic}}_{3\mathcal E}(\mathcal A) \leq C_1 L \frac{Q^2}{|\mathcal K|^3} + C_2 \frac{Q^{2/3}}{|\mathcal K|^{2/3} |\mathcal X|^{1/3}} + C_3 \frac{1}{|\mathcal K|}.$$
>
> For DES parameters — 56-bit keys, 64-bit blocks — the advantage stays small until about $2^{78}$ queries `[BR06]`.

## Example

### Triple-DES

> [!example] Triple-DES
> 3E with $\mathcal E$ = [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] uses keys of $3 \times 56 = 168$ bits `[BS §4.2.3]`. The standard, TDEA, is the E-D-E form: $O = E_{K_3}(D_{K_2}(E_{K_1}(I)))$, decrypted by $D_{K_1}(E_{K_2}(D_{K_3}(\cdot)))$, with three keying options — three independent keys; $K_3 = K_1$; $K_1 = K_2 = K_3$ `[FIPS46-3]`. With three equal keys it computes single DES; this was checked by computation.

## Related

### Constructions
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] — Triple-DES

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Even-Mansour Cipher\|Even-Mansour Cipher]] — lengthens the key by whitening instead of by repeated encryption

### Prerequisites
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]], [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|Ideal Cipher Model]]
