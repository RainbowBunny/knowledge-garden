---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/electronic-codebook-mode/","dg-note-properties":{"aliases":["ECB","ECB Mode"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §4.1.4 (using a block cipher directly for encryption): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents could be read; the definition and the theorem keep the wording of the previous version of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]].

## Syntax

> [!definition] Parameters
> - $\ell \geq 1$: a poly-bounded number of blocks.
> - $m = (m[0], \dots, m[v-1]) \in \mathcal X^{\leq \ell}$: a message of $v \leq \ell$ data blocks.
> - $c \in \mathcal X^{\leq \ell}$: a ciphertext.

> [!definition] Building Blocks
> - $\mathcal E = (\mathsf{KeyGen}, \mathsf{Enc}, \mathsf{Dec})$: any [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|block cipher]] over $(\mathcal K, \mathcal X)$ (universally quantified).

> [!definition] Electronic Codebook Mode
> The **$\ell$-wise ECB cipher** $\mathcal E' = (\mathsf{KeyGen}, \mathsf{Enc}', \mathsf{Dec}')$ is a [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption\|cipher]] over $(\mathcal K, \mathcal X^{\leq \ell}, \mathcal X^{\leq \ell})$, with the key generation of $\mathcal E$:
> - $c \leftarrow \mathsf{Enc}'(k, m)$: (Deterministic) Encryption algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a message $m \in \mathcal X^{\leq \ell}$ with $v = |m|$ blocks.
>     - **Output**: a ciphertext $c \in \mathcal X^{v}$.
>     - **Steps**:
>         1. Returns $c = (\mathsf{Enc}(k, m[0]), \dots, \mathsf{Enc}(k, m[v-1]))$.
> - $m \leftarrow \mathsf{Dec}'(k, c)$: (Deterministic) Decryption algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a ciphertext $c \in \mathcal X^{\leq \ell}$ with $v = |c|$ blocks.
>     - **Output**: a message $m \in \mathcal X^{v}$.
>     - **Steps**:
>         1. Returns $m = (\mathsf{Dec}(k, c[0]), \dots, \mathsf{Dec}(k, c[v-1]))$.
>
> `[BS §4.1.4]`

## Security

> [!security] Semantically secure on messages of distinct blocks `[BS §4.1.4]`
> **Scope**
> - $\mathcal E$: a [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers#Secure Block Cipher\|secure block cipher]].
> - $\mathcal E'$: its $\ell$-wise ECB cipher, with the message space restricted to sequences of at most $\ell$ **distinct** data blocks.
> - $\mathcal A$: a [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Indistinguishability\|semantic security]] adversary against $\mathcal E'$.
>
> ---
> **Property**
> There is a block cipher adversary $\mathcal B$, an elementary wrapper around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{ind\text{-}eav}}_{\mathcal E'}(\mathcal A) = 2 \cdot \mathsf{Adv}^{\mathsf{prp}}_{\mathcal E}(\mathcal B).$$

## Cryptanalysis

> [!attack] Repeated blocks show through
> $\mathsf{Enc}(k, \cdot)$ is deterministic, so equal message blocks give equal ciphertext blocks: $m[i] = m[j]$ iff $c[i] = c[j]$. An adversary who submits $m_0 = (a, a)$ and $m_1 = (a, b)$, $a \neq b$, tells them apart with certainty — which is why the theorem restricts the messages to distinct blocks.

## Related

### Siblings
- [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Randomized Counter Mode\|Symmetric Key Encryption#Randomized Counter Mode]], [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Cipher Block Chaining Mode\|Symmetric Key Encryption#Cipher Block Chaining Mode]] — randomized modes, CPA-secure

### Prerequisites
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers\|Block Ciphers]], [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption\|Symmetric Key Encryption]]
