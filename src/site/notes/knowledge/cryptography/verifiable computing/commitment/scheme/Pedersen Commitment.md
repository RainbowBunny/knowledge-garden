---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/scheme/pedersen-commitment/","dg-note-properties":{}}
---

Reference:
- `[BBB+18]` — B. Bünz, J. Bootle, D. Boneh, A. Poelstra, P. Wuille, G. Maxwell, _Bulletproofs: Efficient Range Proofs for Confidential Transactions_, ePrint 2017/1066, §2.1, Definitions 2, 5 and 6: https://eprint.iacr.org/2017/1066.pdf
- `[DN08]` — I. Damgård, J. B. Nielsen, _Commitment Schemes and Zero-Knowledge Protocols_, lecture notes (2008), Exercise 7 (a commitment from a group homomorphism, $\mathsf{commit}(r, m) = y^m f(r)$): https://homepages.cwi.nl/~schaffne/courses/crypto/2014/papers/ComZK08.pdf
- `[Ped91]` — T. P. Pedersen, _Non-Interactive and Information-Theoretic Secure Verifiable Secret Sharing_, CRYPTO 1991 — the original; not opened.

## Scheme

Reference Name: $\mathsf{Ped}$
Instantiates:: [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]]

### Setting

> [!scheme] Setting
> - $\mathbb G$: a [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|Cyclic Group]] of prime order $p$, written additively: $\mathbf m A$ is the $\mathbf m$-fold sum of $A \in \mathbb G$, for $\mathbf m \in \mathbb Z_p$.
> - $\mathcal M_\mathrm{pp} = \mathbb Z_p$, $\mathcal R_\mathrm{pp} = \mathbb Z_p$, $\mathcal C_\mathrm{pp} = \mathbb G$. `[BBB+18 Def 5]`

### Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]]: Import $(\lambda, \mathrm{pp}, \mathbf m, \mathrm{cm}, \mathrm{st}, r)$; the scheme is randomness-based, $\mathrm{st} = r$.
> - $p$: a prime, the order of $\mathbb G$.
> - $A_\mathrm{com} \in \mathbb G$: the generator that carries the message. $A_\mathrm{hide} \in \mathbb G$: the generator that carries the randomness.

### Algorithms

> [!scheme] Algorithms
> - $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$: (Randomized) Setup algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: $\mathrm{pp} = (\mathbb G, p, A_\mathrm{com}, A_\mathrm{hide})$.
>     - **Steps**:
>         1. Generates a group $\mathbb G$ of prime order $p$.
>         2. Samples $A_\mathrm{com} \xleftarrow{\$} \mathbb G$.
>         3. Samples $A_\mathrm{hide} \xleftarrow{\$} \mathbb G$.
>         4. Returns $\mathrm{pp} = (\mathbb G, p, A_\mathrm{com}, A_\mathrm{hide})$.
> - $(\mathrm{cm}, \mathrm{st}) \leftarrow \mathsf{Commit}(\mathrm{pp}, \mathbf m)$: (Randomized) Commitment algorithm.
>     - **Input**: $\mathrm{pp}$ and a message $\mathbf m \in \mathbb Z_p$.
>     - **Output**: a commitment $\mathrm{cm} \in \mathbb G$ and the decommitment state $\mathrm{st} = r \in \mathbb Z_p$.
>     - **Steps**:
>         1. Parses $\mathrm{pp} = (\mathbb G, p, A_\mathrm{com}, A_\mathrm{hide})$.
>         2. Samples $r \xleftarrow{\$} \mathbb Z_p$.
>         3. Computes $\mathrm{cm} = \mathbf m A_\mathrm{com} + r A_\mathrm{hide}$.
>         4. Returns $(\mathrm{cm}, \mathrm{st})$ with $\mathrm{st} = r$.
> - $b \leftarrow \mathsf{Open}(\mathrm{pp}, (\mathbf m, \mathrm{st}), \mathrm{cm})$: (Deterministic) Opening algorithm.
>     - **Input**: $\mathrm{pp}$, a message $\mathbf m \in \mathbb Z_p$, a decommitment state $\mathrm{st} = r \in \mathbb Z_p$, and a commitment $\mathrm{cm} \in \mathbb G$.
>     - **Output**: $1$ if the opening is valid, $0$ otherwise.
>     - **Steps**:
>         1. Parses $\mathrm{pp} = (\mathbb G, p, A_\mathrm{com}, A_\mathrm{hide})$.
>         2. Returns $1$ if $\mathrm{cm} = \mathbf m A_\mathrm{com} + r A_\mathrm{hide}$, and $0$ otherwise.
>
> `[BBB+18 Def 5]`

> [!remark] Notation in the literature
> The two generators are named by their role: $A_\mathrm{com}$ multiplies the message, $A_\mathrm{hide}$ the randomness — the same names as the matrices of [[knowledge/cryptography/verifiable computing/commitment/scheme/Ajtai Commitment\|Ajtai Commitment]], which has this shape over $\mathbb Z_q$.
>
> | source | form | differences |
> | --- | --- | --- |
> | `[BBB+18 Def 5]` | $\mathsf{Com}(x; r) = g^x h^r$ | multiplicative; $g = A_\mathrm{com}$, $h = A_\mathrm{hide}$; $\mathsf{Setup}$ samples $g, h \xleftarrow{\$} \mathbb G$ |
> | `[DN08 Ex 7]` | $\mathsf{commit}(r, m) = y^m f(r)$ | $f$ a group homomorphism, $y$ an element of prime order $q$ in its image; with $f(r) = g^r$ it reads $y^m g^r$, so $y = A_\mathrm{com}$ and $g = A_\mathrm{hide}$ |

## Property

### Correctness

> [!property] $\mathsf{Ped}$ Correctness
> $\mathsf{Open}$ recomputes $\mathbf m A_\mathrm{com} + r A_\mathrm{hide}$, the value $\mathsf{Commit}$ output, so an honest opening is always accepted; see [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Correctness\|Commitment Scheme#Correctness]].

### Homomorphism

> [!proposition] Additive homomorphism — commitments add like their messages
> For all $\mathbf m_1, \mathbf m_2, r_1, r_2 \in \mathbb Z_p$,
> $$(\mathbf m_1 A_\mathrm{com} + r_1 A_\mathrm{hide}) + (\mathbf m_2 A_\mathrm{com} + r_2 A_\mathrm{hide}) = (\mathbf m_1 + \mathbf m_2) A_\mathrm{com} + (r_1 + r_2) A_\mathrm{hide},$$
> so $\mathsf{Ped}$ is a [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Homomorphism\|homomorphic commitment]] `[BBB+18 Def 2]`.

## Security

### Hiding

> [!security] Perfect hiding
> For every adversary $\mathcal A$ in the [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Hiding\|hiding game]], unbounded included, whenever $A_\mathrm{hide} \neq 0$,
> $$\mathsf{Adv}^\mathsf{hide}_\mathsf{Ped}(\mathcal A) = 0.$$
> `[BBB+18 §2.1]` states perfect hiding for the vector form below, of which this is the case $n = 1$.

> [!proof]
> $\mathbb G$ has prime order, so a nonzero $A_\mathrm{hide}$ generates it and $r \mapsto r A_\mathrm{hide}$ is a bijection $\mathbb Z_p \to \mathbb G$. For uniform $r$, $\mathrm{cm} = \mathbf m A_\mathrm{com} + r A_\mathrm{hide}$ is then uniform on $\mathbb G$ for every $\mathbf m$: Game 0 and Game 1 send identically distributed $\mathrm{cm}$. This is the argument of `[DN08 Ex 7]`: multiplying a uniform element of the subgroup by $y^m$ leaves it uniform.

> [!remark] The zero generator
> $\mathsf{Setup}$ as written in `[BBB+18 Def 5]` samples $A_\mathrm{hide}$ from all of $\mathbb G$, so $A_\mathrm{hide} = 0$ with probability $1/p$; then $\mathrm{cm} = \mathbf m A_\mathrm{com}$ hides nothing. Sampling $A_\mathrm{com}, A_\mathrm{hide}$ from $\mathbb G \setminus \{0\}$ removes the case.

### Binding

> [!security] Computational binding under discrete logarithms
> If the [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption#Claim\|discrete-logarithm assumption]] holds in $\mathbb G$, then $\mathsf{Ped}$ is [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Binding\|computationally binding]] `[BBB+18 §2.1]`: from a binding adversary $\mathcal A$, the reduction $\mathcal B$ below computes $\log_{A_\mathrm{com}} A_\mathrm{hide}$ whenever $\mathcal A$ wins.

> [!proof] Reduction $\mathcal B$
> | | DL challenger | | reduction $\mathcal B$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- | --- | --- |
> | 1 | $x \xleftarrow{\$} \mathbb Z_p$<br>$H = x\, G$ for a generator $G$ | $\xrightarrow{\ G,\, H\ }$ | $A_\mathrm{com} = G$<br>$A_\mathrm{hide} = H$<br>$\mathrm{pp} = (\mathbb G, p, A_\mathrm{com}, A_\mathrm{hide})$ | $\xrightarrow{\ \mathrm{pp}\ }$ | |
> | 2 | | | | $\xleftarrow{\ \mathrm{cm},\, (\mathbf m_0, r_0),\, (\mathbf m_1, r_1)\ }$ | outputs a commitment and two openings |
> | 3 | | $\xleftarrow{\ x'\ }$ | **if** both openings are valid and $\mathbf m_0 \neq \mathbf m_1$:<br>$x' = (\mathbf m_0 - \mathbf m_1)(r_1 - r_0)^{-1} \bmod p$ | | |
>
> **Why $x' = x$.** Two valid openings of $\mathrm{cm}$ give
> $$\mathbf m_0 A_\mathrm{com} + r_0 A_\mathrm{hide} = \mathbf m_1 A_\mathrm{com} + r_1 A_\mathrm{hide},$$
> that is
> $$(\mathbf m_0 - \mathbf m_1)\, G = (r_1 - r_0)\, H.$$
> The left side is nonzero, since $\mathbf m_0 \neq \mathbf m_1$ and $G$ generates $\mathbb G$; so $r_1 \neq r_0$, and $H = (\mathbf m_0 - \mathbf m_1)(r_1 - r_0)^{-1}\, G$. The public parameters $\mathcal B$ sends have the distribution of $\mathsf{Setup}$ conditioned on $A_\mathrm{com} \neq 0$.

## Variant

### Pedersen vector commitment

> [!definition] Parameters
> - $n$: the message length. $\mathbf A_\mathrm{com} = (A_{\mathrm{com},1}, \dots, A_{\mathrm{com},n}) \in \mathbb G^n$: one generator per coordinate.

> [!scheme] Pedersen vector commitment
> $\mathsf{Setup}$ samples $\mathbf A_\mathrm{com} \xleftarrow{\$} \mathbb G^n$ and $A_\mathrm{hide} \xleftarrow{\$} \mathbb G$; a message is $\mathbf m \in \mathbb Z_p^n$, the randomness $r \in \mathbb Z_p$, and
> $$\mathrm{cm} = \sum_{i=1}^n \mathbf m_i A_{\mathrm{com},i} + r A_\mathrm{hide} \in \mathbb G.$$
> It is perfectly hiding and computationally binding under the discrete-logarithm assumption. `[BBB+18 Def 6]`

## Related

### Siblings
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Ajtai Commitment\|Ajtai Commitment]] — the same shape with matrices over $\mathbb Z_q$; the message must then be short
- [[knowledge/cryptography/verifiable computing/commitment/scheme/BDLOP Commitment\|BDLOP Commitment]] — a lattice commitment that, like this one, accepts arbitrary messages

### Prerequisites
- [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]], [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|Cyclic Group]], [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|Discrete-Logarithm Assumption]]
- [[knowledge/cryptography/verifiable computing/proof system/interactive/Sigma Protocols\|Sigma Protocols]] — Okamoto's protocol proves knowledge of an opening $(\alpha, \beta)$ of $g^\alpha h^\beta$
