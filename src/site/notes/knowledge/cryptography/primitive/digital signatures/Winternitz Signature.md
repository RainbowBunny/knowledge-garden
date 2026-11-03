---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/winternitz-signature/","dg-note-properties":{"aliases":["Winternitz One-Time Signature","WOTS"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §14.3 (Winternitz one-time signatures), §14.3.1 (a domination free function): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents of the book could be read; the construction and theorem keep the wording of the note Old Digital Signature, which this note replaces.
- `[Hül13]` — A. Hülsing, _W-OTS+ – Shorter Signatures for Hash-Based Signature Schemes_, AFRICACRYPT 2013, §2.2 (the Winternitz scheme and its checksum), §3.2: https://huelsing.net/wordpress/wp-content/uploads/2013/05/wotsspr.pdf
- `[BDE+11]` — J. Buchmann, E. Dahmen, S. Ereth, A. Hülsing, M. Rückert, _On the Security of the Winternitz One-Time Signature Scheme_, AFRICACRYPT 2011; ePrint 2011/191, abstract: https://eprint.iacr.org/2011/191

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]: Import $(\lambda, \mathcal M, \mathrm{pk}, \mathrm{sk})$.
> - $n$: the number of chains.
> - $d$: the chain length.
> - $I_d = \{0, 1, \dots, d\}$: the positions along a chain.
> - $f^{(j)}$: $f$ applied $j$ times.
> - $P : \mathcal M \to I_d^n$: the message encoding, $P(m) = (s_1, \dots, s_n)$.

> [!definition] Building Blocks
> - $f$: a function over $(\mathcal X, \mathcal X)$, [[knowledge/cryptography/special function/trapdoor function/Trapdoor Functions#One-way on $d$ iterates\|one-way on $d$ iterates]].
> - $G_\mathrm{prg}$: a [[knowledge/cryptography/special function/pseudorandom generator/Pseudorandom Generators\|PRG]] over $(\mathcal S, \mathcal X^n)$.
> - $H$: a [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]] over $(\mathcal X^n, \mathcal T)$.

> [!definition] Winternitz Signature
> $\mathcal S_\mathrm{win} = (\mathsf{KeyGen}, \mathsf{Sign}, \mathsf{Verify})$ over $\mathcal M$:
> - $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: $\mathrm{pk} = H(y_1, \dots, y_n) \in \mathcal T$ and $\mathrm{sk} = k$.
>     - **Steps**:
>         1. $k \xleftarrow{\$} \mathcal S$.
>         2. $(x_1, \dots, x_n) \leftarrow G_\mathrm{prg}(k)$.
>         3. For $i = 1, \dots, n$: $y_i \leftarrow f^{(d)}(x_i)$ — the end of the $i$-th chain.
> - $\sigma \leftarrow \mathsf{Sign}(\mathrm{sk}, m)$: (Deterministic) Signing algorithm.
>     - **Input**: a signing key $\mathrm{sk} = k$ and a message $m \in \mathcal M$.
>     - **Output**: $\sigma = (\sigma_1, \dots, \sigma_n)$.
>     - **Steps**:
>         1. $(x_1, \dots, x_n) \leftarrow G_\mathrm{prg}(k)$.
>         2. $(s_1, \dots, s_n) \leftarrow P(m)$.
>         3. For $i = 1, \dots, n$: $\sigma_i \leftarrow f^{(s_i)}(x_i)$ — $s_i$ steps along the chain.
> - $b \leftarrow \mathsf{Verify}(\mathrm{pk}, m, \sigma)$: (Deterministic) Verification algorithm.
>     - **Input**: a verification key $\mathrm{pk} \in \mathcal T$, a message $m$ and a signature $\sigma = (\sigma_1, \dots, \sigma_n)$.
>     - **Output**: $1$ (accept) or $0$ (reject).
>     - **Steps**:
>         1. $(s_1, \dots, s_n) \leftarrow P(m)$.
>         2. For $i = 1, \dots, n$: $\hat y_i \leftarrow f^{(d - s_i)}(\sigma_i)$ — the rest of the chain.
>         3. Returns $1$ iff $H(\hat y_1, \dots, \hat y_n) = \mathrm{pk}$.
>
> `[BS §14.3]`

## Property

### Correctness

> [!property] Correctness
> $f^{(d - s_i)}(f^{(s_i)}(x_i)) = f^{(d)}(x_i) = y_i$, so the verifier rebuilds $(y_1, \dots, y_n)$ and its hash.

### The requirement on $P$

> [!definition] Domination free
> $P$ is [[knowledge/cryptography/foundations/Cryptographically Special Function#Domination Free Function\|domination free]] if for all distinct $m, m'$ the vector $P(m')$ does not dominate $P(m)$: some coordinate has $s'_i < s_i$ `[BS §14.3]`. A forger would then have to go back along chain $i$, from $f^{(s_i)}(x_i)$ to $f^{(s'_i)}(x_i)$ — inverting $f$.

> [!example] Message digits and a checksum `[Hül13 §2.2]`
> The usual encoding writes the message in base $w$ as $\ell_1$ digits $M_1, \dots, M_{\ell_1}$ and appends the checksum $C = \sum_i (w - 1 - M_i)$ in base $w$, $\ell_2$ more digits. Raising a message digit lowers the checksum, so for any other message some digit is smaller: the checksum makes the encoding domination free. The chains have $w - 1$ steps, the public values are the chain ends, and the signature reveals the $b_i$-th value of chain $i$.

## Security

> [!security] One-time secure `[BS §14.3]`
> **Scope**
> - $f$: one-way on $d$ iterates over $(\mathcal X, \mathcal X)$.
> - $G_\mathrm{prg}$: a [[knowledge/cryptography/special function/pseudorandom generator/Pseudorandom Generators#Secure PRG\|secure PRG]] over $(\mathcal S, \mathcal X^n)$.
> - $H$: [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|collision resistant]] over $(\mathcal X^n, \mathcal T)$.
> - $P : \mathcal M \to I_d^n$: domination free.
> - $\mathcal A$: a signature adversary against $\mathcal S_\mathrm{win}$ that makes at most one signing query.
>
> ---
> **Property**
> There are adversaries $\mathcal B_f$, $\mathcal B_G$, $\mathcal B_H$, elementary wrappers around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathcal S_\mathrm{win}}(\mathcal A) \leq n d \cdot \mathsf{Adv}^{\mathsf{iow}}_{f, d}(\mathcal B_f) + \mathsf{Adv}^{\mathsf{prg}}_{G_\mathrm{prg}}(\mathcal B_G) + \mathsf{Adv}^{\mathsf{cr}}_{H}(\mathcal B_H).$$

> [!remark] A proof from a PRF, withdrawn `[BDE+11]`
> `[BDE+11]` claimed existential unforgeability for Winternitz built from a pseudorandom function family, without collision resistance. Its ePrint page records that ePrint 2017/938 found a flaw in the reduction, which the authors confirm; they recommend W-OTS+ `[Hül13]` instead.

## Related

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/General Lamport Framework\|General Lamport Framework]] — one preimage per selected position instead of a position along a chain
- [[knowledge/cryptography/primitive/digital signatures/Lamport Signature\|Lamport Signature]] — one preimage per message bit, no chains

### Prerequisites
- [[knowledge/cryptography/special function/trapdoor function/Trapdoor Functions#One-way on $d$ iterates\|Trapdoor Functions#One-way on $d$ iterates]], [[knowledge/cryptography/special function/pseudorandom generator/Pseudorandom Generators\|Pseudorandom Generators]], [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]], [[knowledge/cryptography/foundations/Cryptographically Special Function\|Cryptographically Special Function]]
