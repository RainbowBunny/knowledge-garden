---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/hash-and-sign-with-target-collision-resistance/","dg-note-properties":{"aliases":["TCR Hash-and-Sign","Randomized Hash-and-Sign","Hash-and-Sign with TCR"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §13.2.1 (extending the message space using TCR functions): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents of the book could be read; the construction and theorem keep the wording of the note Old Digital Signature, which this note replaces.
- `[HK06]` — S. Halevi, H. Krawczyk, _Strengthening Digital Signatures via Randomized Hashing_, CRYPTO 2006, Introduction and §1.1: https://www.iacr.org/archive/crypto2006/41170039/41170039.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]: Import $(\lambda, \Sigma, \mathrm{pk}, \mathrm{sk})$.
> - $\mathcal M$: the long messages to sign.
> - $\mathcal K_H$: the salt space.
> - $\mathcal T$: the digest space.
> - $r \in \mathcal K_H$: a fresh salt for each signature.

> [!definition] Building Blocks
> - $H$: a keyed [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]] over $(\mathcal K_H, \mathcal M, \mathcal T)$.
> - $\mathsf{SIG} = (\mathsf{KeyGen}, \mathsf{Sign}, \mathsf{Verify})$: any [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|signature scheme]] for short messages in $\mathcal K_H \times \mathcal T$ (universally quantified).

> [!definition] TCR Hash-and-Sign
> $\mathsf{SIG}' = (\mathsf{KeyGen}, \mathsf{Sign}', \mathsf{Verify}')$ for messages in $\mathcal M$, with the same key generation:
> - $\sigma' \leftarrow \mathsf{Sign}'(\mathrm{sk}, m)$: (Randomized) Signing algorithm.
>     - **Input**: a signing key and a message $m \in \mathcal M$.
>     - **Output**: a signature $\sigma' = (\sigma, r)$.
>     - **Steps**:
>         1. $r \xleftarrow{\$} \mathcal K_H$.
>         2. $h \leftarrow H(r, m)$.
>         3. $\sigma \leftarrow \mathsf{Sign}(\mathrm{sk}, (r, h))$ — the salt is signed with the digest.
>         4. Returns $(\sigma, r)$.
> - $b \leftarrow \mathsf{Verify}'(\mathrm{pk}, m, (\sigma, r))$: (Deterministic) Verification algorithm.
>     - **Input**: a verification key, a message $m$ and a signature $(\sigma, r)$.
>     - **Output**: $1$ or $0$.
>     - **Steps**:
>         1. $h \leftarrow H(r, m)$.
>         2. Returns $\mathsf{Verify}(\mathrm{pk}, (r, h), \sigma)$.
>
> `[BS §13.2.1]`. `[HK06]` describes the same: the signer picks a fresh random salt and signs the pair $(r, H_r(M))$.

## Property

### Correctness

> [!property] Correctness
> The verifier recomputes $h = H(r, m)$ from the transmitted salt and checks the signature on $(r, h)$, so honest signatures verify by the correctness of $\mathsf{SIG}$.

## Security

> [!security] Secure, if the scheme is secure and the hash TCR `[BS §13.2.1]`
> **Scope**
> - $\mathsf{SIG}$: [[knowledge/cryptography/primitive/digital signatures/Digital Signature#Unforgeability\|existentially unforgeable]].
> - $H$: [[knowledge/cryptography/special function/hash function/Hash Function#Target Collision Resistance\|target collision resistant]].
> - $\mathcal A$: a signature adversary against $\mathsf{SIG}'$ making at most $Q$ signing queries.
>
> ---
> **Property**
> There are a signature adversary $\mathcal B_\mathsf{SIG}$ and a TCR adversary $\mathcal B_H$, elementary wrappers around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathsf{SIG}'}(\mathcal A) \leq \mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathsf{SIG}}(\mathcal B_\mathsf{SIG}) + Q \cdot \mathsf{Adv}^{\mathsf{tcr}}_{H}(\mathcal B_H).$$

> [!remark] TCR instead of collision resistance `[HK06 Introduction]`
> In the TCR game the attacker commits to its message before the salt is drawn — as the signer draws a fresh $r$ only after a message is chosen. This is a weaker requirement on $H$ than collision resistance. The factor $Q$ comes from guessing which of the signed messages the forgery collides with.

> [!remark] Not signing the salt
> If only $H(r, m)$ is signed and $r$ travels in the clear, TCR no longer suffices: the forger may change the salt as well. An [[knowledge/cryptography/special function/hash function/Hash Function#Enhanced Target Collision Resistance\|enhanced TCR]] hash covers this case `[HK06 Introduction, §1.1]` — [[knowledge/cryptography/primitive/digital signatures/Randomized Lamport Signature\|Randomized Lamport Signature]].

## Related

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/Hash-and-Sign\|Hash-and-Sign]] — no salt, a collision-resistant hash, no factor $Q$

### Prerequisites
- [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]], [[knowledge/cryptography/special function/hash function/Hash Function#Target Collision Resistance\|Hash Function#Target Collision Resistance]]
