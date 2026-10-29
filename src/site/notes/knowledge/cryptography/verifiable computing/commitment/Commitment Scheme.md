---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/commitment-scheme/","dg-note-properties":{}}
---

Reference:
- `[DN08]` — I. Damgård, J. B. Nielsen, _Commitment Schemes and Zero-Knowledge Protocols_, lecture notes (2008), §2: https://homepages.cwi.nl/~schaffne/courses/crypto/2014/papers/ComZK08.pdf
- `[BBB+18]` — B. Bünz, J. Bootle, D. Boneh, A. Poelstra, P. Wuille, G. Maxwell, _Bulletproofs: Efficient Range Proofs for Confidential Transactions_, ePrint 2017/1066, §2.1, Definitions 1–4: https://eprint.iacr.org/2017/1066.pdf
- ePrint 2025/2099 — M. S. Ahmadi, T. Eghlidos, B. Abdolmaleki, N. K. Nguyen, _A Lattice-based Designated Verifier zkSNARK from Standard Assumptions_: https://eprint.iacr.org/2025/2099 — uses commitments; not used for the definitions below.

## Intuition

> [!example] Coin Flipping by Telephone
> Suppose Alice and Bob are getting a divorce but they can not even stand facing each other, so they have to discuss over the phone how to split the furniture, the kids, etc. Since they can not agree who get which, they decide to flip a coin. To make the game fair, we can use a simple protocol:
> 1. Alice commits to a random bit $b_A$, and sends the resulting commitment $\mathrm{cm}$ to Bob.
> 2. Bob chooses a random bit $b_B$ and sends it to Alice.
> 3. Alice opens $\mathrm{cm}$ to let Bob learn $b_A$, and both parties compute the result, which is $b = b_A \oplus b_B$.

> [!remark] The box
> Committing is like putting a message in a locked box and giving the box away: having given it away, the sender cannot change what is inside (*binding*); the receiver cannot tell what is inside until the sender hands over the key (*hiding*). `[DN08 §2.1]`

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter.
> - $\mathrm{pp}$: the public parameters. $\mathrm{td}$: a trapdoor, which some setups also output.
> - $\mathcal M_\mathrm{pp}$: the message space; $\mathcal C_\mathrm{pp}$: the commitment space; $\mathcal R_\mathrm{pp}$: the randomness space of a randomness-based scheme — all fixed by $\mathrm{pp}$.
> - $\mathbf m \in \mathcal M_\mathrm{pp}$: a message. $\mathrm{cm} \in \mathcal C_\mathrm{pp}$: a commitment.
> - $\mathrm{st}$: the decommitment state — what the committer keeps after committing, and reveals to open.
> - $r \in \mathcal R_\mathrm{pp}$: the randomness of a commitment, in a randomness-based scheme.
>
> `[BBB+18 Def 1]`

> [!definition] Commitment Scheme
> A **commitment scheme** is a tuple of efficient algorithms $(\mathsf{Setup}, \mathsf{Commit}, \mathsf{Open})$:
> - $(\mathrm{pp}, \mathrm{td}) \leftarrow \mathsf{Setup}(1^\lambda)$: (Randomized) Setup algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: public parameters $\mathrm{pp}$, which fix $\mathcal M_\mathrm{pp}$, $\mathcal R_\mathrm{pp}$ and $\mathcal C_\mathrm{pp}$ and sometimes trapdoor $\mathrm{td}$.
> - $(\mathrm{cm}, \mathrm{st}) \leftarrow \mathsf{Commit}(\mathrm{pp}, \mathbf m)$: (Randomized) Commitment algorithm.
>     - **Input**: $\mathrm{pp}$ and a message $\mathbf m \in \mathcal M_\mathrm{pp}$.
>     - **Output**: a commitment $\mathrm{cm} \in \mathcal C_\mathrm{pp}$, which is sent, and a decommitment state $\mathrm{st}$, which the committer keeps.
> - $b \leftarrow \mathsf{Open}(\mathrm{pp}, (\mathbf m, \mathrm{st}), \mathrm{cm})$: (Deterministic) Opening algorithm.
>     - **Input**: $\mathrm{pp}$, a claimed message $\mathbf m$ with a decommitment state $\mathrm{st}$, and a commitment $\mathrm{cm}$.
>     - **Output**: $1$ (accept) or $0$ (reject).
>
> `[BBB+18 Def 1]` `[DN08 §2.3]`

> [!definition] Randomness-Based Commitment
> In the common case the decommitment state is the randomness. The scheme fixes a deterministic function $\mathsf{Com}_\mathrm{pp}: \mathcal M_\mathrm{pp} \times \mathcal R_\mathrm{pp} \to \mathcal C_\mathrm{pp}$, and
> - $\mathsf{Commit}$ samples $r \xleftarrow{\$} \mathcal R_\mathrm{pp}$ and returns $\mathrm{cm} = \mathsf{Com}_\mathrm{pp}(\mathbf m; r)$ and $\mathrm{st} = r$;
> - $\mathsf{Open}$ returns $1$ iff $\mathrm{cm} = \mathsf{Com}_\mathrm{pp}(\mathbf m; \mathrm{st})$, possibly after checking that $\mathbf m$ and $\mathrm{st}$ lie in their spaces.
>
> This is the only form `[BBB+18 Def 1]` and `[DN08 §2.3]` define; [[knowledge/cryptography/verifiable computing/commitment/scheme/Pedersen Commitment\|Pedersen Commitment]], [[knowledge/cryptography/verifiable computing/commitment/scheme/Ajtai Commitment\|Ajtai Commitment]] and [[knowledge/cryptography/verifiable computing/commitment/scheme/BDLOP Commitment\|BDLOP Commitment]] have it. `[BBB+18 Def 1]` `[DN08 §2.3]`

> [!remark] The three phases `[DN08 §2.3]`
> - **Set-up** — one party runs $\mathsf{Setup}$ and sends $\mathrm{pp}$ to the other, who checks it and accepts or rejects.
> - **Commit** — the sender runs $\mathsf{Commit}$ on $\mathbf m$, sends $\mathrm{cm}$ and keeps $\mathrm{st}$.
> - **Open** — the sender reveals $(\mathbf m, \mathrm{st})$, and the receiver runs $\mathsf{Open}$.

> [!remark] Notation in the literature
> This note follows the three-algorithm form; both sources below are randomness-based, have two algorithms, and leave $\mathsf{Open}$ as "recompute $\mathsf{Com}_\mathrm{pp}(\mathbf m; r)$ and compare". The message is written $\mathbf m$, the commitment $\mathrm{cm}$, the decommitment state $\mathrm{st}$ (as the verification state $\mathrm{st}$ of [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]]: what a party keeps for a later step), the randomness $r$.
>
> | source | algorithms | differences |
> | --- | --- | --- |
> | `[BBB+18 Def 1]` | $(\mathsf{Setup}, \mathsf{Com})$ | $\mathrm{com} = \mathsf{Com}_\mathrm{pp}(x; r)$ with $r \xleftarrow{\$} \mathcal R_\mathrm{pp}$; no opening algorithm |
> | `[DN08 §2.3]` | generator $G$ and $\mathsf{commit}_\mathrm{pk}(r, b)$ | a public key $\mathrm{pk}$ instead of $\mathrm{pp}$; $r \in \{0, 1\}^l$; bit messages $b \in \{0, 1\}$; the randomness comes first |

## Property

### Correctness

> [!proposition] Correctness — an honest opening is always accepted
> For every $\mathrm{pp}$ output by $\mathsf{Setup}(1^\lambda)$ and every $\mathbf m \in \mathcal M_\mathrm{pp}$,
> $$\mathsf{Open}\big(\mathrm{pp}, (\mathbf m, \mathrm{st}), \mathrm{cm}\big) = 1 \quad \text{where } (\mathrm{cm}, \mathrm{st}) \leftarrow \mathsf{Commit}(\mathrm{pp}, \mathbf m).$$
> For a randomness-based scheme this holds because $\mathsf{Open}$ recomputes the value $\mathrm{cm} = \mathsf{Com}_\mathrm{pp}(\mathbf m; r)$ that $\mathsf{Commit}$ output. `[DN08 §2.3]`

### Homomorphism

> [!definition] Homomorphic Commitment
> A randomness-based scheme is **homomorphic** if $\mathcal M_\mathrm{pp}$, $\mathcal R_\mathrm{pp}$ and $\mathcal C_\mathrm{pp}$ are abelian groups and, for all $\mathbf m_1, \mathbf m_2 \in \mathcal M_\mathrm{pp}$ and $r_1, r_2 \in \mathcal R_\mathrm{pp}$,
> $$\mathsf{Com}_\mathrm{pp}(\mathbf m_1; r_1) + \mathsf{Com}_\mathrm{pp}(\mathbf m_2; r_2) = \mathsf{Com}_\mathrm{pp}(\mathbf m_1 + \mathbf m_2; r_1 + r_2).$$
> `[BBB+18 Def 2]`

## Security

### Binding

> [!definition] Parameters
> - The scheme's $\lambda, \mathrm{pp}, \mathcal M_\mathrm{pp}, \mathrm{cm}, \mathrm{st}$ from Syntax.
> - $\mathbb A$: the [[knowledge/cryptography/foundations/Adversary\|Adversary]] class — probabilistic polynomial time for computational binding, unbounded for perfect binding.

> [!definition] Binding
> ### Scope
> A commitment scheme and the class $\mathbb A$ of Parameters.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ receives $\mathrm{pp}$, produced by $\mathsf{Setup}(1^\lambda)$; no oracle.
> - **Promise** — none.
> - **Quantifier** — $\forall \mathcal A \in \mathbb A$.
> - **Adaptivity** — $\mathcal A$ speaks once, after seeing $\mathrm{pp}$.
>
> ---
> ### Experiment
> A search game with one branch. `[BBB+18 Def 4]` `[DN08 §2.3, type 2]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$ | $\xrightarrow{\ \mathrm{pp}\ }$ | |
> | 2 | | $\xleftarrow{\ \mathrm{cm},\, (\mathbf m_0, \mathrm{st}_0),\, (\mathbf m_1, \mathrm{st}_1)\ }$ | outputs a commitment and two openings |
> | 3 | $b_0 \leftarrow \mathsf{Open}(\mathrm{pp}, (\mathbf m_0, \mathrm{st}_0), \mathrm{cm})$<br>$b_1 \leftarrow \mathsf{Open}(\mathrm{pp}, (\mathbf m_1, \mathrm{st}_1), \mathrm{cm})$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $\mathbf m_0 \neq \mathbf m_1$;
> - $b_0 = 1$;
> - $b_1 = 1$.
>
> ---
> ### Property
> $$\mathsf{Adv}^\mathsf{bind}(\mathcal A) = \Pr[\mathcal A \text{ wins}],$$
> over the coins of $\mathsf{Setup}$ and $\mathcal A$.
> - **Computationally binding**: negligible for every PPT $\mathcal A$. `[BBB+18 Def 4]` `[DN08 §2.3]`
> - **Perfectly binding**: $0$ for every $\mathcal A$. `[BBB+18 Def 4]`

> [!definition] Unconditional Binding
> If $\mathrm{pp}$ is correctly generated, then $\mathbf m$ is uniquely determined by $\mathrm{cm} = \mathsf{Com}_\mathrm{pp}(\mathbf m; r)$: even an unbounded sender cannot change its mind after committing. `[DN08 §2.3, type 1]`

> [!remark] The source's form
> `[BBB+18 Def 4]` lets the adversary output $(x_0, x_1, r_0, r_1)$ and asks for $\mathsf{Com}(x_0; r_0) = \mathsf{Com}(x_1; r_1)$ with $x_0 \neq x_1$: the randomness-based case, with $\mathrm{st}_i = r_i$ and $\mathrm{cm}$ the common value. `[DN08]` calls the adversary $P^*$, a cheating sender.

### Hiding

> [!definition] Parameters
> - The scheme's $\lambda, \mathrm{pp}, \mathcal M_\mathrm{pp}, \mathrm{cm}, \mathrm{st}$ from Syntax.
> - $\mathbb A$: the [[knowledge/cryptography/foundations/Adversary\|Adversary]] class — probabilistic polynomial time for computational hiding, unbounded for statistical or perfect hiding.

> [!definition] Hiding
> ### Scope
> A commitment scheme and the class $\mathbb A$ of Parameters.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ receives $\mathrm{pp}$ and one commitment, never its decommitment state.
> - **Promise** — $\mathbf m_0, \mathbf m_1 \in \mathcal M_\mathrm{pp}$.
> - **Quantifier** — $\forall \mathcal A \in \mathbb A$.
> - **Adaptivity** — $\mathbf m_0, \mathbf m_1$ are chosen after $\mathrm{pp}$ is seen. One challenge.
>
> ---
> ### Experiment
> A distinguishing game: the two branches differ in the committed message only. `[BBB+18 Def 3]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$ | $\xrightarrow{\ \mathrm{pp}\ }$ | |
> | 2 | | $\xleftarrow{\ \mathbf m_0,\, \mathbf m_1\ }$ | chooses $\mathbf m_0, \mathbf m_1 \in \mathcal M_\mathrm{pp}$ |
> | 3 | **Game 0**: $(\mathrm{cm}, \mathrm{st}) \leftarrow \mathsf{Commit}(\mathrm{pp}, \mathbf m_0)$<br>**Game 1**: $(\mathrm{cm}, \mathrm{st}) \leftarrow \mathsf{Commit}(\mathrm{pp}, \mathbf m_1)$ | $\xrightarrow{\ \mathrm{cm}\ }$ | |
> | 4 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\mathsf{Adv}^\mathsf{hide}(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$$
> - **Computationally hiding**: negligible for every PPT $\mathcal A$. `[BBB+18 Def 3]` `[DN08 §2.3, type 1]`
> - **Statistically (unconditionally) hiding**: negligible for every $\mathcal A$; for bit commitments, $\mathsf{commit}_\mathrm{pk}(r, 0) \sim_s \mathsf{commit}_\mathrm{pk}(s, 1)$ for correctly generated $\mathrm{pk}$. `[DN08 §2.3, type 2]`
> - **Perfectly hiding**: $0$ for every $\mathcal A$; the two distributions are identical, $\sim_p$. `[BBB+18 Def 3]` `[DN08 §2.3]`
>
> The relations $\sim_c, \sim_s, \sim_p$ are those of [[knowledge/cryptography/foundations/Indistinguishability\|Indistinguishability]] `[DN08 Def 3]`.

> [!remark] The source's form
> `[BBB+18 Def 3]` samples $b$ and $r \xleftarrow{\$} \mathcal R_\mathrm{pp}$, commits to $\mathbf m_b$ as $\mathsf{Com}(\mathbf m_b; r)$ and bounds $|\Pr[b' = b] - 1/2|$, splitting the adversary into $\mathcal A_{\mathrm{Hiding},1}$ (which outputs the two messages) and $\mathcal A_{\mathrm{Hiding},2}$ (which outputs $b'$). Here the adversary is one stateful machine ([[knowledge/cryptography/foundations/Security Game\|Security Game]]) and the advantage is the difference, twice the source's quantity ([[knowledge/cryptography/primitive/public-key encryption/property/Indistinguishability under Chosen-Plaintext Attack#Bit-guessing form\|Indistinguishability under Chosen-Plaintext Attack#Bit-guessing form]]). `[DN08]` commits to bits, $\mathcal M = \{0, 1\}$, so its game has no message choice: Game $b$ commits to $b$.

## Variant

### The two types, and why not both
- **Type 1** — unconditionally binding, computationally hiding: the sender runs $\mathsf{Setup}$ and sends $\mathrm{pp}$ to the receiver, who verifies it.
- **Type 2** — computationally binding, unconditionally hiding: the receiver runs $\mathsf{Setup}$.
- Both unconditional at once is impossible between two parties, because each sees everything the other sends; it becomes possible in distributed or noisy-channel settings. `[DN08 §2.3]`

## Related

### Instantiations
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Pedersen Commitment\|Pedersen Commitment]] — $\mathbf m A_\mathrm{com} + r A_\mathrm{hide}$ in a group of prime order; perfectly hiding, binding under discrete logarithms
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Ajtai Commitment\|Ajtai Commitment]] — $\mathbf A_\mathrm{com} \mathbf m + \mathbf A_\mathrm{hide} \mathbf r \bmod q$ with binary $\mathbf m, \mathbf r$; statistically hiding, binding under SIS
- [[knowledge/cryptography/verifiable computing/commitment/scheme/BDLOP Commitment\|BDLOP Commitment]] — a module-lattice commitment to arbitrary messages; hiding under Module-LWE, binding under Module-SIS
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Merkle Tree\|Merkle Tree]], [[knowledge/cryptography/verifiable computing/commitment/scheme/From Collision Resistance\|From Collision Resistance]]

### Siblings
- [[knowledge/cryptography/verifiable computing/commitment/Commitment with Linear Decommitment\|Commitment with Linear Decommitment]]
- [[knowledge/cryptography/verifiable computing/commitment/Cryptographic Accumulator\|Cryptographic Accumulator]] — compresses a whole set, with a short witness of membership for each element; deterministic, so not hiding

### Prerequisites
- [[knowledge/cryptography/foundations/Security Game\|Security Game]], [[knowledge/cryptography/foundations/Indistinguishability\|Indistinguishability]], [[knowledge/cryptography/foundations/Adversary\|Adversary]]
