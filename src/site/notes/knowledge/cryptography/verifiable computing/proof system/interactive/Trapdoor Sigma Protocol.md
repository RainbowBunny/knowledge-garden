---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof-system/interactive/trapdoor-sigma-protocol/","dg-note-properties":{"aliases":["Trapdoor Σ-Protocol"]}}
---

Reference:
- `[TNLPS26]` — N. Tran, K. Nguyen, D. Liu, J. Pieprzyk, W. Susilo, _Compact Lattice-Based NIZK Arguments for Set Membership and Ring Signatures without RO_, ePrint 2026/1885 (revision of an ASIACRYPT 2026 paper): §1 (technical overview), §2.1 (Definitions 1 and 2, adapted from its reference [13] by Canetti et al.), §3 (Proposition 1), §4.2 (Proposition 2): https://eprint.iacr.org/2026/1885. Its reference list and appendices were beyond what I could read, so works it cites by number are named here only when the text names them.
- `[Dam10]` — I. Damgård, _On Σ-protocols_, lecture notes, CPT 2010, v2, §4 (the OR construction): https://users-cs.au.dk/~ivan/Sigma.pdf

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter.
> - $\mathcal L = (\mathcal L_\mathsf{zk}, \mathcal L_\mathsf{snd})$: a pair of languages, defined by NP relations $\mathcal R_\mathsf{zk}$ and $\mathcal R_\mathsf{snd}$ ([[knowledge/cryptography/verifiable computing/relation/Effective Relation\|Effective Relation]]).
> - $\mathrm{par}$: public parameters. $\mathsf{info}_\mathcal L$: the description of the language. $\mathrm{crs}_\mathcal L$: the language-dependent reference string. $\mathrm{crs} = (\mathrm{par}, \mathrm{crs}_\mathcal L)$.
> - $\mathsf{Chall}$: the challenge space. $(a, c, z)$: first message, challenge, response.
> - $f$: the bad-challenge function. $\tau_\Sigma \in \{0, 1\}^{\ell_\tau}$: the trapdoor.
>
> `[TNLPS26 §2.1]`

> [!definition] Σ-Protocol in the CRS Model
> Requires:: [[knowledge/cryptography/verifiable computing/proof system/interactive/Sigma Protocols\|Sigma Protocols]].
>
> ---
> A **Σ-protocol** for $\mathcal L = (\mathcal L_\mathsf{zk}, \mathcal L_\mathsf{snd})$ is a tuple $\Pi = (\mathsf{Genpar}, \mathsf{GenL}, \mathcal P, \mathcal V)$:
> - $\mathrm{par} \leftarrow \mathsf{Genpar}(1^\lambda)$: (Randomized) Parameter generation.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: public parameters $\mathrm{par}$.
> - $\mathrm{crs}_\mathcal L \leftarrow \mathsf{GenL}(\mathrm{par}, \mathsf{info}_\mathcal L)$: (Randomized) Language-dependent setup.
>     - **Input**: $\mathrm{par}$ and the language description $\mathsf{info}_\mathcal L$.
>     - **Output**: $\mathrm{crs}_\mathcal L$; the reference string is $\mathrm{crs} = (\mathrm{par}, \mathrm{crs}_\mathcal L)$.
> - $(\mathcal P, \mathcal V)$: a three-move interaction on a statement $x$, with $\mathcal P$ also holding a witness $w$:
>     - $\mathcal P$ sends a first message $a$;
>     - $\mathcal V$ sends a challenge $c \xleftarrow{\$} \mathsf{Chall}$;
>     - $\mathcal P$ sends a response $z$;
>     - $\mathcal V$ outputs $1$ or $0$, computed from $(\mathrm{crs}, x, a, c, z)$.
>
> Completeness and zero knowledge are required on $\mathcal L_\mathsf{zk}$, soundness only on $\mathcal L_\mathsf{snd}$ (below). `[TNLPS26 Def 1]`

> [!remark] A pair of relations, not one
> The difference with [[knowledge/cryptography/verifiable computing/proof system/interactive/Sigma Protocols\|Sigma Protocols]] is the gap between the two languages: the honest prover holds a witness of $\mathcal R_\mathsf{zk}$, but soundness only guarantees membership in the larger, relaxed $\mathcal L_\mathsf{snd}$. Lattice protocols built on rejection sampling need this, because a cheating prover can only be shown to know a longer witness than the honest one — the *relaxed soundness* of Lyubashevsky-type protocols `[TNLPS26 §1, §4.2]`. And there is a reference string, which the trapdoor below lives in.

> [!definition] Trapdoor Σ-Protocol
> A Σ-protocol $\Pi$ with bad-challenge function $f$ (see Special soundness) is a **trapdoor Σ-protocol** if it has two more algorithms:
> - $(\mathrm{crs}_\mathcal L, \tau_\Sigma) \leftarrow \mathsf{TrapGen}(\mathrm{par}, \mathsf{info}_\mathcal L)$: (Randomized) Trapdoor setup.
>     - **Input**: $\mathrm{par}$ and $\mathsf{info}_\mathcal L$.
>     - **Output**: a reference string $\mathrm{crs}_\mathcal L$ together with a trapdoor $\tau_\Sigma \in \{0, 1\}^{\ell_\tau}$.
> - $c \leftarrow \mathsf{BadChallenge}(\tau_\Sigma, \mathrm{crs}, x, a)$: (Deterministic) Bad-challenge computation.
>     - **Input**: the trapdoor, the reference string, a statement $x$ and a first message $a$.
>     - **Output**: a challenge $c \in \mathsf{Chall}$.
>
> They must satisfy CRS indistinguishability and BadChallenge correctness (below). `[TNLPS26 Def 2]`

## Property

### Completeness

> [!definition] Completeness
> For every $(x, w) \in \mathcal R_\mathsf{zk}$, an honest execution on a reference string from $\mathsf{GenL}$ is accepted except with probability $\varepsilon(\lambda)$, the completeness error. `[TNLPS26 Def 1]`

### Special zero knowledge

> [!definition] Special Zero Knowledge
> There is a PPT simulator $\mathsf{ZKSim}(\mathrm{crs}, x, c) \to (a, z)$ such that, for $x \in \mathcal L_\mathsf{zk}$ and any challenge $c$, the triple $(a, c, z)$ is indistinguishable from a real transcript with challenge $c$. `[TNLPS26 Def 1]` Compare [[knowledge/cryptography/verifiable computing/proof system/interactive/Sigma Protocols#Special Honest Verifier Zero Knowledge\|Sigma Protocols#Special Honest Verifier Zero Knowledge]].

### Special soundness

> [!definition] Special Soundness — at most one bad challenge
> For any $\mathrm{crs}$, any $x \notin \mathcal L_\mathsf{snd}$ and any first message $a$, there is at most one challenge
> $$c = f(\mathrm{crs}, x, a)$$
> for which an accepting response $z$ exists. The function $f$ is the **bad-challenge function**. `[TNLPS26 Def 1]`

> [!remark] Not the extractor form
> [[knowledge/cryptography/verifiable computing/proof system/interactive/Sigma Protocols#Special Soundness\|Sigma Protocols#Special Soundness]] asks for a witness extractor from two accepting conversations with different challenges. The form here only counts challenges on false statements; a cheating prover on a false statement wins only if the challenge happens to be $f(\mathrm{crs}, x, a)$, which is what the trapdoor computes.

## Security

### CRS indistinguishability

> [!definition] CRS Indistinguishability
> ### Scope
> A trapdoor Σ-protocol $\Pi$ and a PPT adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ receives $\mathrm{par}$ and one $\mathrm{crs}_\mathcal L$.
> - **Promise** — none.
> - **Quantifier** — $\forall$ PPT $\mathcal A$.
> - **Adaptivity** — none.
>
> ---
> ### Experiment
> A distinguishing game: the branches differ in which algorithm makes $\mathrm{crs}_\mathcal L$. `[TNLPS26 Def 2]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $\mathrm{par} \leftarrow \mathsf{Genpar}(1^\lambda)$<br>**Game 0**: $\mathrm{crs}_\mathcal L \leftarrow \mathsf{GenL}(\mathrm{par}, \mathsf{info}_\mathcal L)$<br>**Game 1**: $(\mathrm{crs}_\mathcal L, \tau_\Sigma) \leftarrow \mathsf{TrapGen}(\mathrm{par}, \mathsf{info}_\mathcal L)$ | $\xrightarrow{\ \mathrm{par},\, \mathrm{crs}_\mathcal L\ }$ | |
> | 2 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $\big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|$ is negligible for every PPT $\mathcal A$.

### BadChallenge correctness

> [!definition] BadChallenge Correctness
> For any $x \notin \mathcal L_\mathsf{snd}$, any $(\mathrm{crs}_\mathcal L, \tau_\Sigma) \leftarrow \mathsf{TrapGen}(\mathrm{par}, \mathsf{info}_\mathcal L)$ and any first message $a$,
> $$\mathsf{BadChallenge}(\tau_\Sigma, \mathrm{crs}, x, a) = f(\mathrm{crs}, x, a).$$
> `[TNLPS26 Def 2]`

## Variant

### Two transformations

> [!remark] From a trapdoor Σ-protocol to a NIZK argument `[TNLPS26 §1, §3]`
> - **Soundness boosting** — a protocol with inverse-polynomial soundness error is run in $\kappa = \Theta(\lambda / \log \lambda)$ parallel copies, with rejection sampling applied jointly to all copies; a rejected attempt restarts with fresh randomness, about $M$ attempts in expectation (the repetition constant of [[knowledge/cryptography/foundations/generic helper/Lattice Helper#Rejection Sampling\|rejection sampling]]).
> - **NIZK compilation** — the compiler of `[TNLPS26]`'s reference [36] turns any trapdoor Σ-protocol into a multi-theorem NIZK argument in the CRS model (`[TNLPS26]` Appendix B). This replaces the [[knowledge/cryptography/verifiable computing/compiler/Fiat-Shamir Transform\|Fiat-Shamir Transform]], whose analysis needs the [[knowledge/cryptography/assumptions/idealized models/Random Oracle Model\|Random Oracle Model]]; see [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]].

## Example

### Linear relations modulo several moduli

> [!example] Multi-moduli trapdoor Σ-protocol `[TNLPS26 §3, Prop 1]`
> - **The problem** — lattice zero-knowledge frameworks built on rejection sampling work over one modulus $q$, while real statements mix components with different moduli (hashes, commitments, encryption). Homogenizing $n_i$ equations modulo $q_i$ into one large modulus $Q$ costs $\sum_i n_i \log(Q / q_i)$ extra bits, and in a Merkle-path proof this recurs at every level `[TNLPS26 §1]`.
> - **Statement** — public linear relations, one per modulus:
>     $$\mathbf t_i = \mathbf M_i \mathbf m \bmod q_i, \qquad i = 0, \dots, l - 1,$$
>     with $\mathbf M_i$ an $n_i \times l_m$ matrix over $\mathcal R_{q_i}$.
> - **Witness** — one short $\mathbf m$, $\lVert \mathbf m \rVert \leq B_m$, with $B_m$ much smaller than every $q_i$.
> - **Idea** — the prover commits to $\mathbf m$ with the extractable mode of the [[knowledge/cryptography/verifiable computing/commitment/scheme/BDLOP Commitment\|BDLOP Commitment]] and answers all relations with one challenge $c$ and one response $\mathbf z_m$, checked as
>     $$\mathbf a_i + c\, \mathbf t_i = \mathbf M_i \mathbf z_m \bmod q_i$$
>     for each $i$. The rejection-sampling step does not depend on $q_i$, so each relation stays at its native modulus.
> - **Proposition 1** — this is a trapdoor Σ-protocol: CRS indistinguishability holds unconditionally (TrapGen outputs what GenL does, plus the trapdoor); completeness has the abort probability of rejection sampling; two accepting responses for distinct challenges give a witness of the relaxed language, and the commitment trapdoor $\mathbf S$ computes the bad challenge by extracting $\mathbf z_m$ and checking the remaining equations; the simulator samples the response from a Gaussian and computes the first message from the challenge.

### Set membership

> [!example] OR-composition along a Merkle path `[TNLPS26 §4.2, Prop 2]`
> To prove that a committed value is a leaf of a lattice Merkle tree ([[knowledge/cryptography/verifiable computing/commitment/Cryptographic Accumulator\|Cryptographic Accumulator]]), each level $i$ needs a disjunction — the node is the left or the right child — proved with the OR technique of [[knowledge/cryptography/verifiable computing/proof system/interactive/Sigma Protocols#OR composition\|Sigma Protocols#OR composition]]. The $\ell$ level-wise protocols share one challenge, a function $\mathsf{BadChallenge}_\mathsf{OR}$ handles the disjunction, and commitments to the intermediate nodes chain the levels. Proposition 2: the result is a trapdoor Σ-protocol for the set-membership language — see [[knowledge/cryptography/verifiable computing/relation/Set Membership Relation\|Set Membership Relation]].

## Related

### Siblings
- [[knowledge/cryptography/verifiable computing/proof system/interactive/Sigma Protocols\|Sigma Protocols]] — the plain three-move protocol for one relation, with extractor-style special soundness

### Constructions
- [[knowledge/cryptography/verifiable computing/relation/Set Membership Relation\|Set Membership Relation]] — the set-membership NIZK of `[TNLPS26]` is built this way
- [[knowledge/cryptography/primitive/digital signatures/Ring Signature\|Ring Signature]] — the standard-model ring signature of `[TNLPS26 §5]`

### Prerequisites
- [[knowledge/cryptography/verifiable computing/relation/Effective Relation\|Effective Relation]], [[knowledge/cryptography/verifiable computing/property/Zero Knowledge\|Zero Knowledge]], [[knowledge/cryptography/verifiable computing/property/Soundness\|Soundness]], [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]]
