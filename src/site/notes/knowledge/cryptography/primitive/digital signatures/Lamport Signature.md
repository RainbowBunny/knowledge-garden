---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/lamport-signature/","dg-note-properties":{"aliases":["Lamport One-Time Signature","Basic Lamport Signature"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §14.1 (basic Lamport signatures): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents of the book could be read; the construction and the bound keep the wording of the note Old Digital Signature, which this note replaces.
- `[Rey9]` — L. Reyzin, _Digital Signatures: Definition and First Constructions. Hashing_, lecture notes, Ch. 9 of BU CAS CS 538, §9.2 (Claims 1 and 2): https://www.cs.bu.edu/~reyzin/teaching/cryptonotes/notes-9.pdf
- `[Lam79]` — L. Lamport, _Constructing Digital Signatures from a One Way Function_, technical report CSL-98, October 1979 — author's page: https://www.microsoft.com/en-us/research/publication/constructing-digital-signatures-one-way-function/

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]: Import $(\lambda, \mathrm{pk}, \mathrm{sk})$, with $\mathcal M = \{0, 1\}^v$, $\Sigma = \mathcal X^v$.
> - $v$: the message length in bits. $m = m_1 \dots m_v \in \{0, 1\}^v$.
> - $x_{i, b} \in \mathcal X$, $y_{i, b} \in \mathcal Y$, for $i = 1, \dots, v$ and $b \in \{0, 1\}$: the secret values and their images.

> [!definition] Building Blocks
> - $f$: any [[knowledge/cryptography/special function/one-way function/One-Way Functions\|one-way function]] over $(\mathcal X, \mathcal Y)$ (universally quantified).

> [!definition] Lamport Signature
> $\mathcal S_L = (\mathsf{KeyGen}, \mathsf{Sign}, \mathsf{Verify})$ over $(\{0, 1\}^v, \mathcal X^v)$:
> - $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: $\mathrm{sk} = (x_{i, b})_{i, b} \in \mathcal X^{2v}$ and $\mathrm{pk} = (y_{i, b})_{i, b} \in \mathcal Y^{2v}$.
>     - **Steps**:
>         1. Samples $x_{i, b} \xleftarrow{\$} \mathcal X$ for $i = 1, \dots, v$ and $b = 0, 1$.
>         2. Sets $y_{i, b} \leftarrow f(x_{i, b})$.
> - $\sigma \leftarrow \mathsf{Sign}(\mathrm{sk}, m)$: (Deterministic) Signing algorithm.
>     - **Input**: $\mathrm{sk}$ and $m \in \{0, 1\}^v$.
>     - **Output**: a signature $\sigma \in \mathcal X^v$.
>     - **Steps**:
>         1. Returns $\sigma = (x_{1, m_1}, \dots, x_{v, m_v})$ — for each bit, the preimage it selects.
> - $b \leftarrow \mathsf{Verify}(\mathrm{pk}, m, \sigma)$: (Deterministic) Verification algorithm.
>     - **Input**: $\mathrm{pk}$, $m \in \{0, 1\}^v$ and $\sigma = (\sigma_1, \dots, \sigma_v) \in \mathcal X^v$.
>     - **Output**: $1$ (accept) or $0$ (reject).
>     - **Steps**:
>         1. Returns $1$ iff $f(\sigma_i) = y_{i, m_i}$ for all $i = 1, \dots, v$.
>
> `[BS §14.1]` `[Rey9 §9.2]`. The case $v = 1$ is the **one-bit Lamport signature** $\mathcal S_\mathrm{1bit}$: $\mathrm{pk} = (f(x_0), f(x_1))$ and the signature on $m \in \{0, 1\}$ is $x_m$.

## Property

### Correctness

> [!property] Correctness
> $\sigma_i = x_{i, m_i}$ and $y_{i, m_i} = f(x_{i, m_i})$, so every check passes.

## Security

> [!security] One-time secure if $f$ is one-way `[BS §14.1]` `[Rey9 §9.2]`
> **Scope**
> - $f$: one-way over $(\mathcal X, \mathcal Y)$.
> - $\mathcal A$: a signature adversary against $\mathcal S_L$ that makes at most one signing query.
>
> ---
> **Property**
> There is an inverter $\mathcal B$ for $f$, an elementary wrapper around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathcal S_L}(\mathcal A) \leq 2v \cdot \mathsf{Adv}^{\mathsf{ow}}_{f}(\mathcal B).$$
> For $v = 1$: $\mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathcal S_\mathrm{1bit}}(\mathcal A) \leq 2 \cdot \mathsf{Adv}^{\mathsf{ow}}_{f}(\mathcal B)$. So $\mathcal S_L$ is a [[knowledge/cryptography/primitive/digital signatures/Digital Signature#Unforgeability\|secure one-time signature]].

> [!proof] Why the factor $2v$ `[Rey9 §9.2]`
> $\mathcal B$ plants its challenge $y$ at a random position $(i, b)$ of the public key. A forgery on $m' \neq m$ differs from the signed $m$ in some bit $i$ and reveals a preimage of $y_{i, m'_i}$, never released; with probability $1/(2v)$ this is the planted position. `[Rey9]` concludes that Lamport's scheme is $2v$ times less secure than the one-way function.

> [!attack] Two signatures break it
> Signatures on $0^v$ and $1^v$ reveal every $x_{i, b}$, after which anyone can sign any message. The key must sign once.

## Variant

> [!remark] The scheme in `[Lam79]` is a subset scheme
> Lamport's report signs a message by revealing 20 of 40 secret keys, the subset chosen by a function of the message — the [[knowledge/cryptography/primitive/digital signatures/General Lamport Framework\|General Lamport Framework]]. On the author's page, Lamport notes that Diffie and Hellman already mention the idea in _New Directions in Cryptography_ (1976).

## Related

### Constructions
- [[knowledge/cryptography/primitive/digital signatures/Randomized Lamport Signature\|Randomized Lamport Signature]] — signs a salted eTCR hash of long messages
- [[knowledge/cryptography/primitive/digital signatures/Hash-and-Sign\|Hash-and-Sign]] — extends the message space with a collision-resistant hash

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/General Lamport Framework\|General Lamport Framework]] — a subset of $n$ preimages per message instead of one of each pair
- [[knowledge/cryptography/primitive/digital signatures/Winternitz Signature\|Winternitz Signature]] — hash chains: fewer values, more evaluations of $f$

### Prerequisites
- [[knowledge/cryptography/special function/one-way function/One-Way Functions\|One-Way Functions]], [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]
