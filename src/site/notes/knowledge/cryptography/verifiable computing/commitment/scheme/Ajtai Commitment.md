---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/scheme/ajtai-commitment/","dg-note-properties":{"aliases":["KTX Commitment","SIS Commitment"]}}
---

Reference:
- `[KTX08]` — A. Kawachi, K. Tanaka, K. Xagawa, _Concurrently Secure Identification Schemes Based on the Worst-Case Hardness of Lattice Problems_, ASIACRYPT 2008, §3 (string commitment; Lemmas 3.1 and 3.2): https://iacr.org/archive/asiacrypt2008/53500376/53500376.pdf
- `[BDOP16]` — C. Baum, I. Damgård, S. Oechsner, C. Peikert, _Efficient Commitments and Zero-Knowledge Protocols from Ring-SIS with Applications to Lattice-based Threshold Cryptosystems_, the version served at ePrint 2016/997, §1.1 (on the KTX scheme): https://eprint.iacr.org/2016/997.pdf
- `[TNLPS26]` — N. Tran, K. Nguyen, D. Liu, J. Pieprzyk, W. Susilo, _Compact Lattice-Based NIZK Arguments for Set Membership and Ring Signatures without RO_, ePrint 2026/1885 (revision of an ASIACRYPT 2026 paper), §4.2: https://eprint.iacr.org/2026/1885

## Scheme

Reference Name: $\mathsf{KTX}$
Instantiates:: [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]]

### Setting

> [!scheme] Setting
> - $\mathbb Z_q$: the integers modulo $q$; matrices over $\mathbb Z_q$ act on binary vectors ([[knowledge/math/number theory/Modular Arithmetic\|Modular Arithmetic]], [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]]).
> - $\mathcal M_\mathrm{pp} = \{0, 1\}^{m/2}$, $\mathcal R_\mathrm{pp} = \{0, 1\}^{m/2}$, $\mathcal C_\mathrm{pp} = \mathbb Z_q^n$. `[KTX08 §3]`

### Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]]: Import $(\lambda, \mathrm{pp}, \mathbf m, \mathrm{cm}, \mathrm{st}, r)$; here the randomness is a vector $\mathbf r$, and $\mathrm{st} = \mathbf r$.
> - [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]]: Import $(n, m, q)$; $m$ is even.
> - The conditions of `[KTX08 Lemma 3.1]`:
>     - $m > 10 n \log q$;
>     - $q \geq 4 m n^{3/2}$.
> - $\mathbf A_\mathrm{hide}, \mathbf A_\mathrm{com} \in \mathbb Z_q^{n \times m/2}$: the two halves of a matrix $\mathbf A = [\mathbf A_\mathrm{hide} \mid \mathbf A_\mathrm{com}] \in \mathbb Z_q^{n \times m}$.

### Algorithms

> [!scheme] Algorithms
> - $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$: (Randomized) Setup algorithm, run by a trusted party.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: $\mathrm{pp} = (n, m, q, \mathbf A_\mathrm{com}, \mathbf A_\mathrm{hide})$.
>     - **Steps**:
>         1. Chooses $n, m, q$ satisfying the conditions of Parameters.
>         2. Samples $\mathbf A \xleftarrow{\$} \mathbb Z_q^{n \times m}$.
>         3. Parses $\mathbf A = [\mathbf A_\mathrm{hide} \mid \mathbf A_\mathrm{com}]$.
>         4. Returns $\mathrm{pp} = (n, m, q, \mathbf A_\mathrm{com}, \mathbf A_\mathrm{hide})$.
> - $(\mathrm{cm}, \mathrm{st}) \leftarrow \mathsf{Commit}(\mathrm{pp}, \mathbf m)$: (Randomized) Commitment algorithm.
>     - **Input**: $\mathrm{pp}$ and a message $\mathbf m \in \{0, 1\}^{m/2}$.
>     - **Output**: a commitment $\mathrm{cm} \in \mathbb Z_q^n$ and the decommitment state $\mathrm{st} = \mathbf r \in \{0, 1\}^{m/2}$.
>     - **Steps**:
>         1. Samples $\mathbf r \xleftarrow{\$} \{0, 1\}^{m/2}$.
>         2. Computes $\mathrm{cm} = \mathbf A_\mathrm{com} \mathbf m + \mathbf A_\mathrm{hide} \mathbf r \bmod q$.
>         3. Returns $(\mathrm{cm}, \mathrm{st})$ with $\mathrm{st} = \mathbf r$.
> - $b \leftarrow \mathsf{Open}(\mathrm{pp}, (\mathbf m, \mathrm{st}), \mathrm{cm})$: (Deterministic) Opening algorithm.
>     - **Input**: $\mathrm{pp}$, a message $\mathbf m$, a decommitment state $\mathrm{st} = \mathbf r$, and a commitment $\mathrm{cm} \in \mathbb Z_q^n$.
>     - **Output**: $1$ if the opening is valid, $0$ otherwise.
>     - **Steps**:
>         1. Checks $\mathbf m \in \{0, 1\}^{m/2}$.
>         2. Checks $\mathbf r \in \{0, 1\}^{m/2}$.
>         3. Returns $1$ if both checks pass and $\mathrm{cm} = \mathbf A_\mathrm{com} \mathbf m + \mathbf A_\mathrm{hide} \mathbf r \bmod q$, and $0$ otherwise.
>
> `[KTX08 §3]`

> [!remark] Notation in the literature
> `[KTX08 §3]` writes $\mathsf{Com}_\mathbf A(s; \rho) = \mathbf A \mathbf x \bmod q$ with $\mathbf x = \rho \circ s$ the concatenation of the random string $\rho$ and the message $s$; splitting $\mathbf A$ into the columns that meet $\rho$ and those that meet $s$ gives $\mathbf A_\mathrm{hide} \rho + \mathbf A_\mathrm{com} s$. `[TNLPS26 §4.2]` calls it the **KTX commitment** and writes $\mathbf c_d = \mathbf C \mathbf d + \mathbf D \mathbf r_d \bmod q_\mathrm{cm}$, over the ring $\mathcal R_{q_\mathrm{cm}}$ rather than $\mathbb Z_q$.

## Property

### Correctness

> [!property] $\mathsf{KTX}$ Correctness
> An honest $\mathbf m$ and $\mathbf r$ are binary and $\mathrm{cm}$ is recomputed exactly, so an honest opening is always accepted; see [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Correctness\|Commitment Scheme#Correctness]].

> [!remark] Why the message must be short
> Binding rests on a short kernel vector (below), so it holds only for openings with short $\mathbf m$: `[BDOP16 §1.1]` notes that the KTX scheme restricts messages to vectors of small norm, because binding is lost otherwise. This is the difference with [[knowledge/cryptography/verifiable computing/commitment/scheme/Pedersen Commitment\|Pedersen Commitment]], whose message is any element of $\mathbb Z_p$, and the reason for [[knowledge/cryptography/verifiable computing/commitment/scheme/BDLOP Commitment\|BDLOP Commitment]].

## Security

> [!security] Statistical hiding and computational binding `[KTX08 Lemma 3.1]`
> Under the conditions of Parameters, if $\mathrm{SIS}_{q, m, \sqrt m}$ is hard on average ([[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution#Search Variant\|Short Integer Solution#Search Variant]]), then $\mathsf{KTX}$ is a statistically [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Hiding\|hiding]] and computationally [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Binding\|binding]] commitment scheme in the trusted-setup model.
> - **Binding** — two valid openings $(\mathbf m, \mathbf r) \neq (\mathbf m', \mathbf r')$ of one $\mathrm{cm}$ are a collision of $\mathbf x \mapsto \mathbf A \mathbf x \bmod q$ on $\{0, 1\}^m$, so $\mathbf z = (\mathbf r - \mathbf r', \mathbf m - \mathbf m')$ is nonzero, has $\lVert \mathbf z \rVert \leq \sqrt m$, and satisfies $\mathbf A \mathbf z = \mathbf 0 \bmod q$ — see [[knowledge/cryptography/special function/hash function/scheme/Ajtai Hash Function\|Ajtai Hash Function]].
> - **Hiding** — for all but a $q^{-n}$ fraction of matrices $\mathbf A$, the commitment of any message is within statistical distance $q^{-n}$ of uniform on $\mathbb Z_q^n$ (a random-subset-sum argument that `[KTX08]` takes from Regev).

## Variant

### Long messages

> [!definition] Parameters
> - $m = 2r$; $\mathbf A = [\mathbf B \mid \mathbf C]$ with $\mathbf B, \mathbf C \in \mathbb Z_q^{n \times r}$. $h_\mathbf C$: the Merkle–Damgård iteration of $f_\mathbf C(\mathbf s) = \mathbf C \mathbf s \bmod q$.

> [!scheme] KTX commitment to strings of any length
> For $s \in \{0, 1\}^*$ and $\rho \in \{0, 1\}^r$,
> $$\mathsf{Com}_\mathbf A(s; \rho) = h_\mathbf C(s) + f_\mathbf B(\rho) \bmod q.$$
> A collision finder for it gives a collision finder for $f_\mathbf A$ `[KTX08 Lemma 3.2]`.

### Module version

Over a ring $\mathcal R_q$ instead of $\mathbb Z_q$, with matrices over $\mathcal R_q$ and short ring vectors: the form used by `[TNLPS26 §4.2]` for the path nodes of its accumulator ([[knowledge/cryptography/verifiable computing/relation/Set Membership Relation\|Set Membership Relation]]).

## Related

### Siblings
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Pedersen Commitment\|Pedersen Commitment]] — the same shape, $\mathbf m A_\mathrm{com} + r A_\mathrm{hide}$, in a group of prime order
- [[knowledge/cryptography/verifiable computing/commitment/scheme/BDLOP Commitment\|BDLOP Commitment]] — lifts the restriction to short messages

### Prerequisites
- [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]], [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]], [[knowledge/cryptography/special function/hash function/scheme/Ajtai Hash Function\|Ajtai Hash Function]]
