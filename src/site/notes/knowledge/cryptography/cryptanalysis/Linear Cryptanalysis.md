---
{"dg-publish":true,"permalink":"/knowledge/cryptography/cryptanalysis/linear-cryptanalysis/","dg-note-properties":{"aliases":["Linear Relation","Linear Attack"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §4.3.1 (algorithmic attacks): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents could be read; the definition and the lemma keep the wording of the previous version of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]].
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §7.2.1, Note 7.6: https://cacr.uwaterloo.ca/hac/about/chap7.pdf

## Definition

> [!definition] Parameters
> - $\mathcal E = (E, D)$: a [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|block cipher]] with $\mathcal X = \{0, 1\}^n$ and $\mathcal K = \{0, 1\}^h$.
> - $m[S] = m[i_1] \oplus \cdots \oplus m[i_\ell]$: the parity of the bits of $m$ in the positions $S = \{i_1, \dots, i_\ell\}$.
> - $S_0, S_1 \subseteq \{0, \dots, n - 1\}$, $S_2 \subseteq \{0, \dots, h - 1\}$: sets of bit positions.
> - $\varepsilon$: the **bias**.

> [!definition] Linear Relation
> $\mathcal E$ has a **linear relation** with bias $\varepsilon$ if for every key $k$ and a uniformly random $m \in \mathcal X$,
> $$\Pr\big[m[S_0] \oplus E(k, m)[S_1] = k[S_2]\big] \geq \frac{1}{2} + \varepsilon,$$
> for a non-negligible $\varepsilon$. For an ideal cipher, plaintext and ciphertext behave like independent strings: the relation holds with probability exactly $1/2$, and $\varepsilon = 0$. `[BS §4.3.1]`

## Property

> [!lemma] Majority vote — enough known pairs reveal one key parity
> **Scope**
> - $\mathcal E$: a block cipher with a linear relation $(S_0, S_1, S_2)$ of bias $\varepsilon$.
> - $m_1, \dots, m_t$: independent uniform messages; $c_i = E(k, m_i)$.
>
> ---
> **Property**
> $$\Pr\Big[k[S_2] = \mathrm{Majority}_{i = 1}^{t}\big(m_i[S_0] \oplus c_i[S_1]\big)\Big] \geq 1 - e^{-t \varepsilon^2 / 2}.$$
>
> `[BS §4.3.1]`. So $t$ of the order of $1 / \varepsilon^2$ known plaintext–ciphertext pairs recover the bit $k[S_2]$ with high probability.

> [!remark] Cost `[HAC Note 7.6]`
> For linear cryptanalysis of DES, the complexity of the attack is essentially its data complexity: the number of known plaintext–ciphertext pairs it needs.

## Related

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers#Implications and a generic attack\|Exhaustive search]] — the generic attack, against which a linear relation is a shortcut

### Prerequisites
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]], [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|Ideal Cipher Model]]
