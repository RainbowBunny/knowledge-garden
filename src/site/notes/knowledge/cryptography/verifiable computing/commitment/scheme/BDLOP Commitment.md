---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/scheme/bdlop-commitment/","dg-note-properties":{}}
---

Reference:
- `[LNS22]` — V. Lyubashevsky, N. K. Nguyen, M. Plançon, _Lattice-Based Zero-Knowledge Proofs and Applications: Shorter, Simpler, and More General_, ePrint 2022/284, §1.3, Equation (4): https://eprint.iacr.org/2022/284
- `[ALS20]` — T. Attema, V. Lyubashevsky, G. Seiler, _Practical Product Proofs for Lattice Commitments_, ePrint 2020/517, §2.4–2.5 and Lemma 4.3: https://eprint.iacr.org/2020/517.pdf
- `[BDOP16]` — C. Baum, I. Damgård, S. Oechsner, C. Peikert, _Efficient Commitments and Zero-Knowledge Protocols from Ring-SIS with Applications to Lattice-based Threshold Cryptosystems_, the version served at ePrint 2016/997, §4.1, Lemmas 2–3: https://eprint.iacr.org/2016/997.pdf
- `[TNLPS26]` — N. Tran, K. Nguyen, D. Liu, J. Pieprzyk, W. Susilo, _Compact Lattice-Based NIZK Arguments for Set Membership and Ring Signatures without RO_, ePrint 2026/1885, §3 and §4.2 (the extractable commitment; its full description is in Appendix A.4, which I could not read): https://eprint.iacr.org/2026/1885
- `[BDLOP18]` — C. Baum, I. Damgård, V. Lyubashevsky, S. Oechsner, C. Peikert, _More Efficient Commitments from Structured Lattice Assumptions_, SCN 2018, LNCS 11035, pp. 368–385 — the source of the name; not opened (its ePrint entry, 2016/997, serves the 2016 version `[BDOP16]`).
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Scheme

Reference Name: $\mathsf{BDLOP}$
Instantiates:: [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]]

### Setting

> [!scheme] Setting
> - $\mathcal R_q$: a polynomial ring modulo $q$ ([[knowledge/math/algebra/structures/polynomial/Polynomial Ring\|Polynomial Ring]], [[knowledge/math/algebra/structures/polynomial/Quotient of Polynomial Ring\|Quotient of Polynomial Ring]]); vectors and matrices over $\mathcal R_q$ ([[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]]).
> - $\chi$: a distribution of short ring vectors; `[ALS20 §2.4]` uses the centered binomial distribution on $\{-1, 0, 1\}$ coefficients.
> - $\mathcal M_\mathrm{pp} = \mathcal R_q^\ell$ — any message modulo $q$; $\mathcal R_\mathrm{pp}$: short vectors in $\mathcal R_q^k$; $\mathcal C_\mathrm{pp} = \mathcal R_q^{n + \ell}$. `[LNS22 §1.3]`

### Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]]: Import $(\lambda, \mathrm{pp}, \mathbf m, \mathrm{cm}, \mathrm{st}, r)$; here the randomness is a vector $\mathbf r$, and $\mathrm{st} = \mathbf r$.
> - $n$: the height of the binding part; $\ell$: the message length; $k$: the randomness length.
> - $\mathbf A \in \mathcal R_q^{n \times k}$: the binding matrix. $\mathbf B \in \mathcal R_q^{\ell \times k}$: the matrix that masks the message.
> - $\beta$: the norm bound an opening must meet.

### Algorithms

> [!scheme] Algorithms
> - $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$: (Randomized) Setup algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: $\mathrm{pp} = (q, \mathbf A, \mathbf B)$.
>     - **Steps**:
>         1. Samples $\mathbf A \xleftarrow{\$} \mathcal R_q^{n \times k}$.
>         2. Samples $\mathbf B \xleftarrow{\$} \mathcal R_q^{\ell \times k}$.
>         3. Returns $\mathrm{pp} = (q, \mathbf A, \mathbf B)$.
> - $(\mathrm{cm}, \mathrm{st}) \leftarrow \mathsf{Commit}(\mathrm{pp}, \mathbf m)$: (Randomized) Commitment algorithm.
>     - **Input**: $\mathrm{pp}$ and a message $\mathbf m \in \mathcal R_q^\ell$.
>     - **Output**: a commitment $\mathrm{cm} = (\mathbf t_A, \mathbf t_B) \in \mathcal R_q^n \times \mathcal R_q^\ell$ and the decommitment state $\mathrm{st} = \mathbf r$.
>     - **Steps**:
>         1. Samples $\mathbf r \leftarrow \chi^k$.
>         2. Computes $\begin{bmatrix} \mathbf t_A \\ \mathbf t_B \end{bmatrix} = \begin{bmatrix} \mathbf A \\ \mathbf B \end{bmatrix} \mathbf r + \begin{bmatrix} \mathbf 0 \\ \mathbf m \end{bmatrix} \bmod q$.
>         3. Returns $(\mathrm{cm}, \mathrm{st})$ with $\mathrm{cm} = (\mathbf t_A, \mathbf t_B)$ and $\mathrm{st} = \mathbf r$.
> - $b \leftarrow \mathsf{Open}(\mathrm{pp}, (\mathbf m, \mathrm{st}), \mathrm{cm})$: (Deterministic) Opening algorithm.
>     - **Input**: $\mathrm{pp}$, a message $\mathbf m \in \mathcal R_q^\ell$, a decommitment state $\mathrm{st} = \mathbf r$, and $\mathrm{cm} = (\mathbf t_A, \mathbf t_B)$.
>     - **Output**: $1$ if the opening is valid, $0$ otherwise.
>     - **Steps**:
>         1. Checks $\lVert \mathbf r \rVert \leq \beta$.
>         2. Checks $\mathbf t_A = \mathbf A \mathbf r \bmod q$.
>         3. Checks $\mathbf t_B = \mathbf B \mathbf r + \mathbf m \bmod q$.
>         4. Returns $1$ if all three hold, and $0$ otherwise.
>
> `[LNS22 §1.3, Eq. (4)]`

> [!remark] Only the randomness is short
> The decommitment state is $\mathbf r$ alone — it determines $\mathbf m = \mathbf t_B - \mathbf B \mathbf r$ — and only $\mathbf r$ must be short; $\mathbf m$ has arbitrary coefficients modulo $q$ `[LNS22 §1.3]`. Compare [[knowledge/cryptography/verifiable computing/commitment/scheme/Ajtai Commitment\|Ajtai Commitment]], where the message also enters the binding equation and must be short.

> [!remark] Notation in the literature
> | source | form | differences |
> | --- | --- | --- |
> | `[LNS22 §1.3, Eq. (4)]` | $\begin{bmatrix} \mathbf A \\ \mathbf B \end{bmatrix} \mathbf s + \begin{bmatrix} \mathbf 0 \\ \mathbf m \end{bmatrix} = \begin{bmatrix} \mathbf t_A \\ \mathbf t_B \end{bmatrix} \bmod q$ | randomness $\mathbf s$; no dimensions fixed there |
> | `[ALS20 §2.5]` | $\mathbf t_0 = \mathbf B_0 \mathbf r$, $t_i = \langle \mathbf b_i, \mathbf r \rangle + m_i$ | $\mathbf B_0 \in \mathcal R_q^{\mu \times (\lambda + \mu + 3)}$, three message slots with rows $\mathbf b_1, \mathbf b_2, \mathbf b_3$; $\mathbf r \leftarrow \chi^{(\lambda + \mu + 3) d}$; called "a variant of" `[BDLOP18]` |
> | `[BDOP16 §4.1]` | $\mathsf{Com}(x; \mathbf r) = \mathbf A \mathbf r + (0, x)^\top \in \mathcal R_q^2$ | one ring element of message; $\mathbf A \in \mathcal R_q^{2 \times k}$; Ring-SIS only |

## Property

### Correctness

> [!property] $\mathsf{BDLOP}$ Correctness
> An honest $\mathbf r \leftarrow \chi^k$ meets the norm bound $\beta$ (for $\beta$ chosen above the support of $\chi^k$), and both equations are recomputed exactly; see [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Correctness\|Commitment Scheme#Correctness]].

### Homomorphism

> [!proposition] Additive homomorphism — commitments add like their messages
> The map $(\mathbf m, \mathbf r) \mapsto \begin{bmatrix} \mathbf A \\ \mathbf B \end{bmatrix} \mathbf r + \begin{bmatrix} \mathbf 0 \\ \mathbf m \end{bmatrix}$ is linear, so the sum of two commitments is a commitment to $\mathbf m_1 + \mathbf m_2$ with randomness $\mathbf r_1 + \mathbf r_2$ — whose norm is up to twice as large, which the bound $\beta$ must allow.

## Security

> [!security] Hiding under Module-LWE
> $\mathsf{BDLOP}$ is computationally [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Hiding\|hiding]] under [[knowledge/cryptography/assumptions/lattice-based/LWE/Module Learning With Error#Decision Module Learning With Error\|Module-LWE]]: hiding follows from $\big(\begin{bmatrix} \mathbf A \\ \mathbf B \end{bmatrix}, \begin{bmatrix} \mathbf A \\ \mathbf B \end{bmatrix} \mathbf r\big)$ being indistinguishable from uniform. `[LNS22 §1.3]` `[ALS20 §2.5]`

> [!security] Binding under Module-SIS
> $\mathsf{BDLOP}$ is computationally [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme#Binding\|binding]] under Module-SIS for $\mathbf A$ (the module form of [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]]): two valid openings $\mathbf r \neq \mathbf r'$ of one $\mathrm{cm}$ give $\mathbf A(\mathbf r - \mathbf r') = \mathbf 0 \bmod q$ with $\lVert \mathbf r - \mathbf r' \rVert \leq 2\beta$. `[LNS22 §1.3]` `[ALS20 §2.5]`

## Variant

### Relaxed opening

> [!definition] Parameters
> - $\bar c$: a nonzero difference of two challenges of a Σ-protocol; invertible in $\mathcal R_q$ for the challenge sets used.

> [!definition] Relaxed Opening
> A relaxed opening of $\mathrm{cm} = (\mathbf t_A, \mathbf t_B)$ is a triple $(\bar c, \mathbf r^*, \mathbf m^*)$ with
> - $\bar c\, \mathbf t_A = \mathbf A \mathbf r^*$;
> - $\bar c\, \mathbf t_B = \mathbf B \mathbf r^* + \bar c\, \mathbf m^*$;
> - $\mathbf r^*$ of norm at most a larger bound than an honest opening.
>
> It is what a zero-knowledge proof of opening extracts, and binding still holds against relaxed openings. `[ALS20 §2.5, Def 4.2, Lemma 4.3]` `[BDOP16 §4.1, Lemma 2]`

### Extractable mode

> [!definition] Parameters
> - $p$: a prime. $\mathbf S \in \mathcal R_q^{\ell \times n}$: the trapdoor matrix. $\mathbf E$: an error matrix with $\lVert \mathbf E \rVert_\infty \leq B_\tau$.

> [!definition] Two Setup Modes
> `[TNLPS26 §4.2]` (with the details in its Appendix A.4) runs the same commitment under two setups:
> - **$\mathsf{Setup}$ (normal mode)** — $(\mathbf A, \mathbf B)$ as above; the commitment is statistically hiding.
> - **$\mathsf{ExtSetup}$ (extraction mode)** — outputs $(\mathbf A, \mathbf B)$ with $\mathbf B = \mathbf S \mathbf A + p \mathbf E \bmod q$, and the trapdoor $(\mathbf S, p)$; the commitment is computationally hiding and extractable.

> [!proposition] Extraction identity — the trapdoor strips the mask
> In extraction mode, for $\mathrm{cm} = \begin{bmatrix} \mathbf A \\ \mathbf B \end{bmatrix} \mathbf r + \begin{bmatrix} \mathbf 0 \\ \mathbf m \end{bmatrix}$,
> $$[-\mathbf S \;\; \mathbf I]\, \mathrm{cm} = p \mathbf E \mathbf r + \mathbf m \bmod q.$$
> `[TNLPS26 §4.2]` uses this equation, with a challenge difference $\bar c$ in front of $\mathrm{cm}$, in the relaxed language of its set-membership protocol.
>
> ⚠️ CLAUDE – verify: from the identity, $\mathbf m$ is recovered as $([-\mathbf S \;\; \mathbf I] \mathrm{cm} \bmod q) \bmod p$ when $\lVert p \mathbf E \mathbf r + \mathbf m \rVert_\infty < q/2$ and $\lVert \mathbf m \rVert_\infty < p/2$; these conditions are mine, the extraction algorithm itself is in Appendix A.4 of `[TNLPS26]`.

> [!proof]
> $[-\mathbf S \;\; \mathbf I]\, \mathrm{cm} = -\mathbf S \mathbf A \mathbf r + \mathbf B \mathbf r + \mathbf m = -\mathbf S \mathbf A \mathbf r + \mathbf S \mathbf A \mathbf r + p \mathbf E \mathbf r + \mathbf m = p \mathbf E \mathbf r + \mathbf m \bmod q$.

## Related

### Siblings
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Ajtai Commitment\|Ajtai Commitment]] — the message enters the binding part and must be short
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Pedersen Commitment\|Pedersen Commitment]] — the group-based scheme with the same "mask plus message" shape

### Constructions
- [[knowledge/cryptography/verifiable computing/proof system/interactive/Trapdoor Sigma Protocol\|Trapdoor Sigma Protocol]] — the multi-moduli protocol of `[TNLPS26 §3]` commits to its witness with the extractable mode

### Prerequisites
- [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]], [[knowledge/cryptography/assumptions/lattice-based/LWE/Module Learning With Error\|Module Learning With Error]], [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]]
