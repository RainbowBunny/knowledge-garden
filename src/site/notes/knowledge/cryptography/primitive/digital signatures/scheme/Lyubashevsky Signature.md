---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/scheme/lyubashevsky-signature/","dg-note-properties":{"aliases":["Lattice Signatures Without Trapdoors","SIS Signature"]}}
---

Reference:
- `[Lyu12]` — V. Lyubashevsky, _Lattice Signatures Without Trapdoors_, EUROCRYPT 2012; ePrint 2011/537: §4, Figure 1 (the scheme), Figure 2 (parameters), Theorem 4.1: https://www.iacr.org/archive/eurocrypt2012/72370731/72370731.pdf · https://eprint.iacr.org/2011/537

## Scheme

Reference Name: $\mathsf{Lyu}$
Instantiates:: [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]

### Setting

> [!scheme] Setting
> - $\mathbb Z_q$: the integers modulo $q$; vectors and matrices over $\mathbb Z_q$ and over $\mathbb Z$.
> - $D_\sigma^m$: the discrete Gaussian distribution on $\mathbb Z^m$ centred at $\mathbf 0$ with standard deviation $\sigma$; $D_{\mathbf v, \sigma}^m$: the same centred at $\mathbf v$ — [[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution\|Discrete Gaussian Distribution]].

### Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]: Import $(\lambda, \mathrm{pk}, \mathrm{sk})$, with messages $\mu \in \{0, 1\}^*$ and signatures $(\mathbf z, \mathbf c)$.
> - $n, m, k$: dimensions; $q$: the modulus; $d$: the bound on the secret entries.
> - $\kappa$: the weight of the challenge, large enough that $H$ has at least $2^{100}$ possible outputs `[Lyu12 Fig 2]`.
> - $\sigma$: the Gaussian parameter, $\sigma \approx 12 d \kappa \sqrt m$; $M$: the rejection constant, about $2.72$ for the parameters of `[Lyu12 Fig 2]`.

### Building Blocks

> [!definition] Building Blocks
> - $H : \{0, 1\}^* \to \{\mathbf v \in \{-1, 0, 1\}^k : \|\mathbf v\|_1 \leq \kappa\}$: a [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]], modeled as a [[knowledge/cryptography/assumptions/idealized models/Random Oracle Model\|random oracle]].

### Algorithms

> [!scheme] Algorithms
> - $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: $\mathrm{sk} = \mathbf S$ and $\mathrm{pk} = (\mathbf A, \mathbf T)$.
>     - **Steps**:
>         1. $\mathbf S \xleftarrow{\$} \{-d, \dots, 0, \dots, d\}^{m \times k}$.
>         2. $\mathbf A \xleftarrow{\$} \mathbb Z_q^{n \times m}$.
>         3. $\mathbf T \leftarrow \mathbf A \mathbf S \in \mathbb Z_q^{n \times k}$.
> - $(\mathbf z, \mathbf c) \leftarrow \mathsf{Sign}(\mathrm{sk}, \mu)$: (Randomized) Signing algorithm.
>     - **Input**: $\mathbf S$ (and $\mathbf A$) and a message $\mu$.
>     - **Output**: a signature $(\mathbf z, \mathbf c)$.
>     - **Steps**:
>         1. $\mathbf y \leftarrow D_\sigma^m$.
>         2. $\mathbf c \leftarrow H(\mathbf A \mathbf y, \mu)$.
>         3. $\mathbf z \leftarrow \mathbf S \mathbf c + \mathbf y$, over $\mathbb Z$.
>         4. With probability $\min\Big(\dfrac{D_\sigma^m(\mathbf z)}{M \cdot D_{\mathbf S \mathbf c, \sigma}^m(\mathbf z)}, 1\Big)$ return $(\mathbf z, \mathbf c)$; otherwise restart.
> - $b \leftarrow \mathsf{Verify}(\mathrm{pk}, \mu, (\mathbf z, \mathbf c))$: (Deterministic) Verification algorithm.
>     - **Input**: a verification key $(\mathbf A, \mathbf T)$, a message $\mu$ and a signature $(\mathbf z, \mathbf c)$.
>     - **Output**: $1$ (accept) or $0$ (reject).
>     - **Steps**:
>         1. Returns $1$ iff $\|\mathbf z\| \leq 2\sigma\sqrt m$ and $\mathbf c = H(\mathbf A \mathbf z - \mathbf T \mathbf c, \mu)$.
>
> `[Lyu12 Fig 1]`

## Property

### Correctness

> [!property] $\mathsf{Lyu}$ Correctness `[Lyu12 Thm 4.1]`
> $\mathbf A \mathbf z - \mathbf T \mathbf c = \mathbf A(\mathbf S \mathbf c + \mathbf y) - \mathbf A \mathbf S \mathbf c = \mathbf A \mathbf y$, so the hash check passes; the norm check passes for an honest signature with probability at least $1 - 2^{-m}$. The signer outputs a signature with probability about $1/M$ per attempt.

### Rejection sampling

> [!remark] Why reject
> Without step 4, $\mathbf z = \mathbf S \mathbf c + \mathbf y$ would follow a Gaussian centred at $\mathbf S \mathbf c$ and leak the secret. Accepting with the stated probability makes the output distributed as $D_\sigma^m$, independent of $\mathbf S$ — which is how `[Lyu12]` avoids trapdoors.

## Security

> [!security] Unforgeable under SIS, in the random oracle model `[Lyu12 Thm 4.1]`
> **Scope**
> - $\mathcal A$: a polynomial-time [[knowledge/cryptography/primitive/digital signatures/Digital Signature#Unforgeability\|forger]] making at most $s$ signing queries and $h$ random-oracle queries, succeeding with probability $\delta$.
>
> ---
> **Property**
> A polynomial-time algorithm solves $\ell_2$-[[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|$\mathrm{SIS}_{q, n, m, \beta}$]] for
> $$\beta = (4\sigma + 2 d \kappa)\sqrt m = \tilde O(d n)$$
> with probability about $\delta^2 / (2(h + s))$.

## Related

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/scheme/Dilithium\|Dilithium]] — a lattice signature over module lattices
- [[knowledge/cryptography/primitive/digital signatures/ID and Signatures from Sigma\|ID and Signatures from Sigma]] — the same commit–challenge–response shape, made non-interactive with a hash

### Prerequisites
- [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]], [[knowledge/cryptography/assumptions/idealized models/Random Oracle Model\|Random Oracle Model]], [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]
