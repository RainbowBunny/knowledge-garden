---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/general-lamport-framework/","dg-note-properties":{"aliases":["Generalized Lamport Signature","Subset Lamport Signature"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §14.2 (a general Lamport framework), §14.2.1 (an explicit containment free function): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents of the book could be read; the construction and theorem keep the wording of the note Old Digital Signature, which this note replaces.
- `[Lam79]` — L. Lamport, _Constructing Digital Signatures from a One Way Function_, technical report CSL-98, October 1979, §2: https://www.microsoft.com/en-us/research/wp-content/uploads/2016/12/Constructing-Digital-Signatures-from-a-One-Way-Function.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]: Import $(\lambda, \mathcal M, \mathrm{pk}, \mathrm{sk})$.
> - $n$: the number of secret values. $x_1, \dots, x_n \in \mathcal X$ and $y_i = f(x_i) \in \mathcal Y$.
> - $P$: a function from $\mathcal M$ to subsets of $\{1, \dots, n\}$; $P(m) = \{s_1, \dots, s_\ell\}$.

> [!definition] Building Blocks
> - $f$: any [[knowledge/cryptography/special function/one-way function/One-Way Functions\|one-way function]] over $(\mathcal X, \mathcal Y)$.
> - $F$: a [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|PRF]] over $(\mathcal K, \{1, \dots, n\}, \mathcal X)$ — it derives the secret values from a short key.

> [!definition] General Lamport Framework
> $\mathcal S_P = (\mathsf{KeyGen}, \mathsf{Sign}, \mathsf{Verify})$ over $\mathcal M$:
> - $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: $\mathrm{pk} = (y_1, \dots, y_n)$ and $\mathrm{sk} = k$.
>     - **Steps**:
>         1. $k \xleftarrow{\$} \mathcal K$.
>         2. For $i = 1, \dots, n$: $x_i \leftarrow F(k, i)$, $y_i \leftarrow f(x_i)$.
> - $\sigma \leftarrow \mathsf{Sign}(\mathrm{sk}, m)$: (Deterministic) Signing algorithm.
>     - **Input**: a signing key $\mathrm{sk} = k$ and a message $m \in \mathcal M$.
>     - **Output**: $\sigma = (\sigma_1, \dots, \sigma_\ell)$.
>     - **Steps**:
>         1. $\{s_1, \dots, s_\ell\} \leftarrow P(m)$.
>         2. For $j = 1, \dots, \ell$: $\sigma_j \leftarrow F(k, s_j)$.
> - $b \leftarrow \mathsf{Verify}(\mathrm{pk}, m, \sigma)$: (Deterministic) Verification algorithm.
>     - **Input**: $\mathrm{pk}$, $m$ and $\sigma = (\sigma_1, \dots, \sigma_u)$.
>     - **Output**: $1$ (accept) or $0$ (reject).
>     - **Steps**:
>         1. $\{s_1, \dots, s_\ell\} \leftarrow P(m)$.
>         2. Returns $1$ iff $u = \ell$ and $f(\sigma_j) = y_{s_j}$ for all $j = 1, \dots, \ell$.
>
> `[BS §14.2]`

## Property

### The requirement on $P$

> [!definition] Containment free
> $P$ is [[knowledge/cryptography/foundations/Cryptographically Special Function#Containment Free Function\|containment free]] if $P(m) \not\subseteq P(m')$ for all distinct $m, m' \in \mathcal M$ — a signature on $m'$ never contains a signature on $m$. `[BS §14.2]`

> [!example] Lamport's 20-of-40 subsets `[Lam79 §2]`
> The report uses 40 keys and lets the message select a 20-element subset; restricting $P$ to subsets of one fixed size is what keeps one subset from containing another. Lamport notes that 40 and 20 could be any $2n$ and $n$. The [[knowledge/cryptography/primitive/digital signatures/Lamport Signature\|Lamport Signature]] is the case of $2v$ values where $P(m)$ picks one value of each pair.

## Security

> [!security] One-time secure `[BS §14.2]`
> **Scope**
> - $f$: one-way over $(\mathcal X, \mathcal Y)$.
> - $F$: a [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Secure PRF\|secure PRF]] over $(\mathcal K, \{1, \dots, n\}, \mathcal X)$.
> - $P$: containment free.
> - $\mathcal A$: a signature adversary against $\mathcal S_P$ that makes at most one signing query.
>
> ---
> **Property**
> There are an inverter $\mathcal B_f$ and a PRF adversary $\mathcal B_F$, elementary wrappers around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathcal S_P}(\mathcal A) \leq n \cdot \mathsf{Adv}^{\mathsf{ow}}_{f}(\mathcal B_f) + \mathsf{Adv}^{\mathsf{prf}}_{F}(\mathcal B_F).$$

> [!proof] Why containment freeness
> After a signature on $m$, a forgery on $m' \neq m$ must reveal $x_s$ for some $s \in P(m') \setminus P(m)$, a set that is nonempty because $P(m') \not\subseteq P(m)$; that $x_s$ was never released, so it is a preimage under $f$.

## Related

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/Lamport Signature\|Lamport Signature]] — the case of pairs, one value per message bit
- [[knowledge/cryptography/primitive/digital signatures/Winternitz Signature\|Winternitz Signature]] — the same idea along hash chains, with domination freeness in place of containment freeness

### Prerequisites
- [[knowledge/cryptography/special function/one-way function/One-Way Functions\|One-Way Functions]], [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|Pseudorandom Function]], [[knowledge/cryptography/foundations/Cryptographically Special Function\|Cryptographically Special Function]]
