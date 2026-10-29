---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/scheme/ajtai-hash-function/","dg-note-properties":{"aliases":["SIS Hash Function"]}}
---

Reference:
- `[Pei16]` — C. Peikert, _A Decade of Lattice Cryptography_, Foundations and Trends in Theoretical Computer Science 10(4), 2016; ePrint 2015/939, §4.1.1: https://eprint.iacr.org/2015/939
- `[KTX08]` — A. Kawachi, K. Tanaka, K. Xagawa, _Concurrently Secure Identification Schemes Based on the Worst-Case Hardness of Lattice Problems_, ASIACRYPT 2008, §3 (the function $f_\mathbf A$ and its collision resistance, used for a commitment): https://iacr.org/archive/asiacrypt2008/53500376/53500376.pdf
- `[Ajt96]` — M. Ajtai, _Generating Hard Instances of Lattice Problems_, STOC 1996 — the original; not opened.

## Scheme

Reference Name: $f_\mathbf A$
Instantiates:: [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]

### Setting

> [!scheme] Setting
> - $\mathbb Z_q^{n \times m}$: matrices modulo $q$, acting on binary vectors ([[knowledge/math/number theory/Modular Arithmetic\|Modular Arithmetic]], [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]]).
> - Domain $\{0, 1\}^m$, range $\mathbb Z_q^n$.

### Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]]: Import $(n, m, q)$, with $m > n \log q$.
> - $\mathbf A \in \mathbb Z_q^{n \times m}$: the key.

### Algorithms

> [!scheme] Algorithms
> - $\mathbf A \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: a key $\mathbf A \in \mathbb Z_q^{n \times m}$.
>     - **Steps**:
>         1. Chooses $n, m, q$ with $m > n \log q$.
>         2. Samples $\mathbf A \xleftarrow{\$} \mathbb Z_q^{n \times m}$.
>         3. Returns $\mathbf A$.
> - $\mathbf y \leftarrow f_\mathbf A(\mathbf x)$: (Deterministic) Hash algorithm.
>     - **Input**: the key $\mathbf A$ and $\mathbf x \in \{0, 1\}^m$.
>     - **Output**: $\mathbf y = \mathbf A \mathbf x \bmod q \in \mathbb Z_q^n$.
>
> `[Pei16 §4.1.1]` `[KTX08 §3]`

## Property

### Compression

> [!proposition] Compression — more inputs than outputs
> Since $m > n \log q$, the domain has $2^m > q^n$ elements, more than the range. `[Pei16 §4.1.1]`

## Security

### Collision resistance

> [!security] Collision resistance from SIS
> For a uniform key, a collision $\mathbf x \neq \mathbf x' \in \{0, 1\}^m$ with $f_\mathbf A(\mathbf x) = f_\mathbf A(\mathbf x')$ gives
> $$\mathbf A(\mathbf x - \mathbf x') = \mathbf 0 \bmod q,$$
> with $\mathbf z = \mathbf x - \mathbf x' \in \{-1, 0, 1\}^m$ nonzero and $\lVert \mathbf z \rVert \leq \sqrt m$: a solution of the [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution#Search Variant\|SIS search game]] with $\beta = \sqrt m$. So any [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|collision finder]] for the keyed family is an SIS adversary with the same advantage. `[Pei16 §4.1.1]` `[KTX08 §3]`

> [!remark] A key, then the collision game
> [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|Hash Function#Collision Resistance]] is stated for a keyless function. For this family the challenger first samples $\mathbf A$ and sends it, then the adversary outputs $\mathbf x, \mathbf x'$; the winning conditions are the same.

> [!remark] Not a commitment
> $f_\mathbf A$ is deterministic and has no randomness input, so $f_\mathbf A(\mathbf x)$ reveals which of two known inputs was hashed: it is binding but not hiding. Adding a random half to the input gives the [[knowledge/cryptography/verifiable computing/commitment/scheme/Ajtai Commitment\|Ajtai Commitment]] `[KTX08 §3]`.

## Related

### Constructions
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Ajtai Commitment\|Ajtai Commitment]] — $f_\mathbf A$ on (randomness, message)
- [[knowledge/cryptography/verifiable computing/commitment/Cryptographic Accumulator\|Cryptographic Accumulator]] — Merkle trees of two-input SIS hashes, $\mathsf{bin}(\mathbf A_0 \mathbf u_0 + \mathbf A_1 \mathbf u_1 \bmod q)$

### Prerequisites
- [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]], [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]], [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution Problem#Application\|Short Integer Solution Problem#Application]]
