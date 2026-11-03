---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/compression-function/scheme/two-input-lattice-hash/","dg-note-properties":{"aliases":["Lattice Merkle Hash","Two-to-One Lattice Hash"]}}
---

Reference:
- `[TNLPS26]` — N. Tran, K. Nguyen, D. Liu, J. Pieprzyk, W. Susilo, _Compact Lattice-Based NIZK Arguments for Set Membership and Ring Signatures without RO_, ePrint 2026/1885, §4.1: Definition 7, Lemma 1: https://eprint.iacr.org/2026/1885
- `[LNWX18]` — S. Ling, K. Nguyen, H. Wang, Y. Xu, _Lattice-Based Group Signatures: Achieving Full Dynamicity (and Deniability) with Ease_, extended version of an ACNS 2017 paper, arXiv 1801.08737: Definition 5 and Lemma 1 (the binary hash of Libert, Ling, Nguyen and Wang): https://arxiv.org/pdf/1801.08737

## Scheme

Reference Name: $f_\mathbf H$
Instantiates:: [[knowledge/cryptography/special function/compression function/Compression Functions\|Compression Functions]]

> [!scheme] Setting
> - $\mathcal R_{q_H}$: a polynomial ring modulo $q_H$ — [[knowledge/math/algebra/structures/polynomial/Quotient of Polynomial Ring\|Quotient of Polynomial Ring]].
> - Vectors and matrices over $\mathcal R_{q_H}$.
> - $\mathcal C_\beta$: the ring elements whose coefficients are bounded by $\beta$.
> - $\mathsf{dec}_B$: base-$B$ decomposition, with gadget matrix $\mathbf G_B$: $\mathsf{dec}_B(\mathbf v) = \mathbf u$ means $\mathbf G_B \mathbf u = \mathbf v$ ([[knowledge/math/algebra/structures/lattice/Lattice Gadget Algorithm\|Lattice Gadget Algorithm]]).

> [!definition] Parameters
> - $n$: the module rank.
> - $q_H$: the modulus.
> - $B > 1$: the base.
> - $\beta = B - 1$: the largest base-$B$ digit.
> - $k_H = \lceil \log_B q_H \rceil$: the number of base-$B$ digits.
> - $m = 2 n k_H$: the width of the key.
> - $\mathbf H = [\mathbf H_0 \mid \mathbf H_1] \in \mathcal R_{q_H}^{n \times m}$, with $\mathbf H_0, \mathbf H_1 \in \mathcal R_{q_H}^{n \times n k_H}$: the key.
>
> `[TNLPS26 §4.1]`

> [!scheme] Two-Input Lattice Hash
> - $\mathbf H \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: a key $\mathbf H \in \mathcal R_{q_H}^{n \times m}$.
>     - **Steps**:
>         1. Chooses $q_H, n, B$.
>         2. Samples $\mathbf H \xleftarrow{\$} \mathcal R_{q_H}^{n \times m}$.
> - $\mathbf u \leftarrow f_\mathbf H(\mathbf u_0, \mathbf u_1)$: (Deterministic) Hash algorithm.
>     - **Input**: the key $\mathbf H$ and two blocks $\mathbf u_0, \mathbf u_1 \in \mathcal C_\beta^{n k_H}$.
>     - **Output**: one block $\mathbf u \in \mathcal C_\beta^{n k_H}$.
>     - **Steps**:
>         1. Returns $\mathbf u = \mathsf{dec}_B(\mathbf H_0 \mathbf u_0 + \mathbf H_1 \mathbf u_1 \bmod q_H)$.
>
> `[TNLPS26 Def 7]`

## Property

### Two blocks in, one block out

> [!proposition] Output in the input domain — the hash can be iterated along a tree
> $f_\mathbf H$ maps $(\mathcal C_\beta^{n k_H})^2$ to $\mathcal C_\beta^{n k_H}$: two blocks to one block of the same shape. The decomposition $\mathsf{dec}_B$ is what brings the output, an element of $\mathcal R_{q_H}^n$, back into short digits, so that it can be the input of the next level of a [[knowledge/cryptography/verifiable computing/commitment/scheme/Merkle Tree\|Merkle Tree]] — the use of [[knowledge/cryptography/verifiable computing/commitment/Cryptographic Accumulator#Lattice Merkle-tree accumulator\|Cryptographic Accumulator#Lattice Merkle-tree accumulator]]. `[TNLPS26 §4.1]`

### A linear relation

> [!proposition] Hashing as a linear equation — what a zero-knowledge proof can check
> By the definition of $\mathsf{dec}_B$,
> $$f_\mathbf H(\mathbf u_0, \mathbf u_1) = \mathbf u \iff \mathbf H_0 \mathbf u_0 + \mathbf H_1 \mathbf u_1 = \mathbf G_B \mathbf u \bmod q_H,$$
> a linear relation between short vectors, as `[LNWX18 Def 5]` states for $B = 2$. A proof of a Merkle path proves one such equation per level; the set-membership protocol of `[TNLPS26 §4.2]` does it inside a [[knowledge/cryptography/verifiable computing/proof system/interactive/Trapdoor Sigma Protocol\|Trapdoor Sigma Protocol]].

## Security

> [!security] Collision resistance under Module-SIS `[TNLPS26 Lemma 1]`
> Under $\mathsf{MSIS}^{(\infty)}_{n, m, \beta, q_H}$ — the module, $\ell_\infty$ form of [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]] — the family $\{f_\mathbf H\}$ is [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|collision resistant]], for a uniform key $\mathbf H$.

> [!proof] Why
> $\mathsf{dec}_B$ is injective, since $\mathbf G_B\, \mathsf{dec}_B(\mathbf v) = \mathbf v$. Two different inputs with the same output therefore give
> $$\mathbf H_0 (\mathbf u_0 - \mathbf u_0') + \mathbf H_1 (\mathbf u_1 - \mathbf u_1') = \mathbf 0 \bmod q_H,$$
> a nonzero short vector in the kernel of $\mathbf H$: a Module-SIS solution.

## Variant

### The binary original

> [!definition] Parameters
> - $n = O(\lambda)$, $q = \tilde O(n^{1.5})$, $k = \lceil \log_2 q \rceil$, $m = 2nk$.
> - $\mathbf A = [\mathbf A_0 \mid \mathbf A_1] \in \mathbb Z_q^{n \times m}$.
> - $\mathsf{bin}$: binary decomposition, with the powers-of-2 matrix $\mathbf G$.

> [!scheme] Binary SIS hash `[LNWX18 Def 5]`
> $$h_\mathbf A(\mathbf u_0, \mathbf u_1) = \mathsf{bin}(\mathbf A_0 \mathbf u_0 + \mathbf A_1 \mathbf u_1 \bmod q) \in \{0, 1\}^{nk},$$
> for $\mathbf u_0, \mathbf u_1 \in \{0, 1\}^{nk}$. It satisfies $h_\mathbf A(\mathbf u_0, \mathbf u_1) = \mathbf u$ iff $\mathbf A_0 \mathbf u_0 + \mathbf A_1 \mathbf u_1 = \mathbf G \mathbf u \bmod q$, and the Merkle-tree accumulator built from it is secure under $\mathrm{SIS}^\infty_{n, m, q, 1}$ `[LNWX18 Lemma 1]`. The base-$B$ form above, over a module, trades hash size against the assumption `[TNLPS26 abstract]`.

## Related

### Constructions
- [[knowledge/cryptography/verifiable computing/commitment/Cryptographic Accumulator\|Cryptographic Accumulator]] — the Merkle-tree accumulator of its Example section
- [[knowledge/cryptography/verifiable computing/relation/Set Membership Relation\|Set Membership Relation]] — proving a Merkle path in zero knowledge, one linear equation per level

### Siblings
- [[knowledge/cryptography/special function/hash function/scheme/Ajtai Hash Function\|Ajtai Hash Function]] — one binary input, no decomposition: compressing, but its output cannot be fed back in
- [[knowledge/cryptography/special function/compression function/scheme/Syndrome Based Compression Function\|Syndrome Based Compression Function]], [[knowledge/cryptography/special function/compression function/scheme/Fast Syndrome Based Compression Function\|Fast Syndrome Based Compression Function]] — the code-based analogues, $\mathbf H \mathbf x^\top$ on a low-weight $\mathbf x$

### Prerequisites
- [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]], [[knowledge/math/algebra/structures/lattice/Lattice Gadget Algorithm\|Lattice Gadget Algorithm]], [[knowledge/cryptography/verifiable computing/commitment/scheme/Merkle Tree\|Merkle Tree]]
