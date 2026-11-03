---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/randomized-lamport-signature/","dg-note-properties":{"aliases":["Lamport Signature with Enhanced TCR"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §14.1.1 (shrinking the signature using an enhanced TCR): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents of the book could be read; the construction keeps the wording of the note Old Digital Signature, which this note replaces; that note stated no theorem for it.
- `[HK06]` — S. Halevi, H. Krawczyk, _Strengthening Digital Signatures via Randomized Hashing_, CRYPTO 2006, Introduction and §1.1: https://www.iacr.org/archive/crypto2006/41170039/41170039.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/digital signatures/Lamport Signature\|Lamport Signature]]: Import $(v, \mathrm{pk}, \mathrm{sk})$.
> - $\mathcal M$: the long messages to sign.
> - $\mathcal R$: the salt space.
> - $r \in \mathcal R$: a fresh salt for each signature.

> [!definition] Building Blocks
> - $\mathcal S_L = (\mathsf{KeyGen}, \mathsf{Sign}, \mathsf{Verify})$: the [[knowledge/cryptography/primitive/digital signatures/Lamport Signature\|Lamport Signature]] on $\{0, 1\}^v$.
> - $H_\mathrm{etcr}$: a keyed [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]] over $(\mathcal R, \mathcal M, \{0, 1\}^v)$.

> [!definition] Randomized Lamport Signature
> $\mathcal S' = (\mathsf{KeyGen}, \mathsf{Sign}', \mathsf{Verify}')$ for messages in $\mathcal M$, with the key generation of $\mathcal S_L$:
> - $\sigma \leftarrow \mathsf{Sign}'(\mathrm{sk}, M)$: (Randomized) Signing algorithm.
>     - **Input**: a signing key and a message $M \in \mathcal M$.
>     - **Output**: a signature $\sigma = (r, \sigma')$.
>     - **Steps**:
>         1. $r \xleftarrow{\$} \mathcal R$.
>         2. $m \leftarrow H_\mathrm{etcr}(r, M) \in \{0, 1\}^v$.
>         3. $\sigma' \leftarrow \mathsf{Sign}(\mathrm{sk}, m)$ — the salt itself is not signed.
>         4. Returns $(r, \sigma')$.
> - $b \leftarrow \mathsf{Verify}'(\mathrm{pk}, M, (r, \sigma'))$: (Deterministic) Verification algorithm.
>     - **Input**: a verification key, a message $M \in \mathcal M$ and a signature $(r, \sigma')$.
>     - **Output**: $1$ (accept) or $0$ (reject).
>     - **Steps**:
>         1. $m \leftarrow H_\mathrm{etcr}(r, M)$.
>         2. Returns $\mathsf{Verify}(\mathrm{pk}, m, \sigma')$.
>
> `[BS §14.1.1]`

## Security

> [!security] What the salt needs `[HK06 Introduction, §1.1]`
> **Scope**
> - $\mathcal S_L$: a secure one-time signature — [[knowledge/cryptography/primitive/digital signatures/Lamport Signature#Security\|Lamport Signature#Security]].
> - $H_\mathrm{etcr}$: [[knowledge/cryptography/special function/hash function/Hash Function#Enhanced Target Collision Resistance\|enhanced target collision resistant]].
>
> ---
> **Property**
> Since only $H_\mathrm{etcr}(r, M)$ is signed and $r$ travels in the clear, a forger may choose a new salt $r'$ along with a new message; enhanced TCR is the property strong enough for a signature on $H_r(M)$ alone to be secure `[HK06]`. `⚠️ CLAUDE – verify:` no bound is stated here, since the previous version of this note gave none.

> [!remark] Why it shrinks the signature `[BS §14.1.1]`
> Lamport signs $v$ bits with $v$ preimages, and $v$ is the digest length: a salted hash, which needs only eTCR, allows a shorter digest than a collision-resistant hash would — the point of signing $H_\mathrm{etcr}(r, M)$ instead of $H(M)$. `⚠️ CLAUDE – verify:` this reason is mine, read off the section title.

## Related

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/Hash-and-Sign with Target Collision Resistance\|Hash-and-Sign with Target Collision Resistance]] — signs the salt with the digest, and needs only TCR
- [[knowledge/cryptography/primitive/digital signatures/Hash-and-Sign\|Hash-and-Sign]] — no salt, a collision-resistant hash

### Prerequisites
- [[knowledge/cryptography/primitive/digital signatures/Lamport Signature\|Lamport Signature]], [[knowledge/cryptography/special function/hash function/Hash Function#Enhanced Target Collision Resistance\|Hash Function#Enhanced Target Collision Resistance]]
