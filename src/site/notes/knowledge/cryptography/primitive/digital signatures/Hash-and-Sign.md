---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/hash-and-sign/","dg-note-properties":{"aliases":["Hash-and-Sign Paradigm","Hash-then-Sign"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §13.2 (extending the message space with collision resistant hashing): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents of the book could be read; the construction and theorem keep the wording of the note Old Digital Signature, which this note replaces.
- `[Rey9]` — L. Reyzin, _Digital Signatures: Definition and First Constructions. Hashing_, lecture notes, Ch. 9 of BU CAS CS 538, §9.4: https://www.cs.bu.edu/~reyzin/teaching/cryptonotes/notes-9.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]: Import $(\lambda, \mathcal M, \Sigma, \mathrm{pk}, \mathrm{sk})$.
> - $\mathcal M'$: the new message space, much larger than $\mathcal M$.

> [!definition] Building Blocks
> - $\mathsf{SIG} = (\mathsf{KeyGen}, \mathsf{Sign}, \mathsf{Verify})$: any [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|signature scheme]] over $(\mathcal M, \Sigma)$ (universally quantified).
> - $H : \mathcal M' \to \mathcal M$: a [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]].

> [!definition] Hash-and-Sign
> $\mathsf{SIG}' = (\mathsf{KeyGen}, \mathsf{Sign}', \mathsf{Verify}')$ over $(\mathcal M', \Sigma)$, with the same key generation:
> - $\sigma \leftarrow \mathsf{Sign}'(\mathrm{sk}, m)$: (Randomized) Signing algorithm.
>     - **Input**: a signing key and a message $m \in \mathcal M'$.
>     - **Output**: a signature $\sigma \in \Sigma$.
>     - **Steps**:
>         1. Returns $\mathsf{Sign}(\mathrm{sk}, H(m))$.
> - $b \leftarrow \mathsf{Verify}'(\mathrm{pk}, m, \sigma)$: (Deterministic) Verification algorithm.
>     - **Input**: a verification key, a message $m \in \mathcal M'$ and a signature $\sigma$.
>     - **Output**: $1$ or $0$.
>     - **Steps**:
>         1. Returns $\mathsf{Verify}(\mathrm{pk}, H(m), \sigma)$.
>
> `[BS §13.2]` `[Rey9 §9.4]`

> [!remark] Why it matters `[BS §13.2]`
> The new scheme signs much larger messages than the original one, so it suffices to build signatures for a small message space, such as 256-bit strings.

> [!remark] Notation in the literature
> `[Rey9 §9.4]` uses a keyed collision-resistant family: the hash index $i$ is chosen at key generation and stored in the public key, and the scheme signs $H_i(m)$.

## Property

### Correctness

> [!property] Correctness
> $\mathsf{Verify}'(\mathrm{pk}, m, \mathsf{Sign}'(\mathrm{sk}, m)) = \mathsf{Verify}(\mathrm{pk}, H(m), \mathsf{Sign}(\mathrm{sk}, H(m))) = 1$, by the correctness of $\mathsf{SIG}$.

## Security

> [!security] Secure, if the scheme is secure and the hash collision resistant `[BS §13.2]` `[Rey9 §9.4]`
> **Scope**
> - $\mathsf{SIG}$: [[knowledge/cryptography/primitive/digital signatures/Digital Signature#Unforgeability\|existentially unforgeable]].
> - $H$: [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|collision resistant]].
> - $\mathcal A$: a signature adversary against $\mathsf{SIG}'$.
>
> ---
> **Property**
> There are a signature adversary $\mathcal B_\mathsf{SIG}$ and a collision finder $\mathcal B_H$, elementary wrappers around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathsf{SIG}'}(\mathcal A) \leq \mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathsf{SIG}}(\mathcal B_\mathsf{SIG}) + \mathsf{Adv}^{\mathsf{cr}}_{H}(\mathcal B_H).$$

> [!proof] Why
> A forgery $(m, \sigma)$ on a new $m$ either has $H(m) = H(m_i)$ for some signed $m_i \neq m$ — a collision — or $H(m)$ is new, and $(H(m), \sigma)$ is a forgery against $\mathsf{SIG}$.

## Related

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/Hash-and-Sign with Target Collision Resistance\|Hash-and-Sign with Target Collision Resistance]] — a randomized hash that needs only target collision resistance

### Prerequisites
- [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]], [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]
