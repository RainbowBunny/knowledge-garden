---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/digital-signature/","dg-note-properties":{"aliases":["Digital Signature Scheme","Signature Scheme","SIG"]}}
---

Reference:
- `[GMR88]` — S. Goldwasser, S. Micali, R. L. Rivest, _A Digital Signature Scheme Secure Against Adaptive Chosen-Message Attacks_, SIAM J. Comput. 17(2), 1988, pp. 281–308: https://people.csail.mit.edu/rivest/pubs/GMR88.pdf (§2.1 syntax, §2.2 attacks, §2.3 breaks).
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, Ch. 13: §13.1 (definition), §13.1.1 (secure signatures), §13.1.2 (mathematical details): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents of the book could be read; the games keep the wording of the previous version of this note, checked against `[GMR88]`, `[ADR02]` and `[AABN02]`.
- `[ADR02]` — J. H. An, Y. Dodis, T. Rabin, _On the Security of Joint Signature and Encryption_, EUROCRYPT 2002, §2.2 (strong unforgeability): https://cims.nyu.edu/~dodis/ps/signcrypt.pdf
- `[AABN02]` — M. Abdalla, J. H. An, M. Bellare, C. Namprempre, _From Identification to Signatures via the Fiat–Shamir Transform_, EUROCRYPT 2002; full version ePrint 2002/022, Def 2.2 (unforgeability in the random-oracle model): https://eprint.iacr.org/2002/022

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter, given to $\mathsf{KeyGen}$ in unary.
> - $\mathcal M$: the message space.
> - $\Sigma$: the signature space.
> - $(\mathrm{pk}, \mathrm{sk})$: a key pair — the public **verification key** and the secret **signing key**.

> [!definition] Digital Signature Scheme
> A **digital signature scheme** $\mathsf{SIG} = (\mathsf{KeyGen}, \mathsf{Sign}, \mathsf{Verify})$ defined over $(\mathcal M, \Sigma)$ is a triple of efficient algorithms:
> - $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: a verification key $\mathrm{pk}$ and a signing key $\mathrm{sk}$.
> - $\sigma \leftarrow \mathsf{Sign}(\mathrm{sk}, m)$: (Randomized) Signing algorithm.
>     - **Input**: a signing key $\mathrm{sk}$ and a message $m \in \mathcal M$.
>     - **Output**: a signature $\sigma \in \Sigma$.
> - $b \leftarrow \mathsf{Verify}(\mathrm{pk}, m, \sigma)$: (Deterministic) Verification algorithm.
>     - **Input**: a verification key $\mathrm{pk}$, a message $m \in \mathcal M$ and a signature $\sigma \in \Sigma$.
>     - **Output**: $1$ (accept) or $0$ (reject).
>
> `[BS §13.1]` `[GMR88 §2.1]`

> [!remark] Notation in the literature
> The form above is the most general one in these sources: $\mathsf{Sign}$ may be randomized, $\mathsf{Verify}$ is deterministic.
>
> | source | algorithms | differences |
> | --- | --- | --- |
> | `[GMR88 §2.1]` | $(G, \sigma, V)$ | $G$ on input $1^k$; $\sigma(M, S_A)$ and $V(S, M, P_A)$, the message before the key; a **signature bound** $B$ on the number of signatures one key may produce; $\sigma$ may take further inputs, such as the number of messages signed so far |
> | `[BS §13.1]` | $(G, S, V)$ | $G$ takes no input; $V$ outputs accept or reject; the scheme is *defined over* $(\mathcal M, \Sigma)$ |
> | `[BS §13.1.2]` | $(G, S, V)$ | the asymptotic form: families $\{\mathcal M_{\lambda, \Lambda}\}$, $\{\Sigma_{\lambda, \Lambda}\}$ with a system parameter $\Lambda$; all three algorithms take $\lambda, \Lambda$ |
>
> The vault calls key generation $\mathsf{KeyGen}$ whatever the source writes.

> [!remark] Attacks and breaks `[GMR88 §2.2–2.3]`
> `[GMR88]` grades the attacker's access — key-only, known-message, generic chosen-message, directed chosen-message, adaptive chosen-message — and its success — total break (the secret key), universal forgery (any message), selective forgery (a message chosen in advance), existential forgery (some message). The game in Security grants the strongest access and asks for the weakest success.

## Property

### Correctness

> [!definition] Correctness
> For every $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$ and every $m \in \mathcal M$,
> $$\Pr\big[\mathsf{Verify}(\mathrm{pk}, m, \mathsf{Sign}(\mathrm{sk}, m)) = 1\big] = 1.$$
> `[BS §13.1]`

## Security

### Unforgeability

> [!definition] Parameters
> - The scheme's $\mathsf{SIG}$, $\lambda$, $\mathcal M$, $\Sigma$ from Syntax.
> - $\mathcal A$: an efficient [[knowledge/cryptography/foundations/Adversary\|Adversary]], one stateful machine.
> - $Q$: a bound on the number of its signing queries.
> - $m_i \in \mathcal M$: the $i$-th signing query.
> - $\sigma_i \in \Sigma$: its answer.
> - $(m, \sigma) \in \mathcal M \times \Sigma$: the candidate forgery.

> [!definition] Existential Unforgeability under Chosen-Message Attack
> ### Scope
> A signature scheme $\mathsf{SIG}$ and an efficient adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ gets $\mathrm{pk}$ and a signature $\sigma_i \leftarrow \mathsf{Sign}(\mathrm{sk}, m_i)$ on each message $m_i$ it asks for; never $\mathrm{sk}$. It is a **$Q$-query adversary** if it asks at most $Q$ times.
> - **Promise** — none.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — an adaptive chosen-message attack: each $m_i$ may depend on $\mathrm{pk}$ and on $\sigma_1, \dots, \sigma_{i-1}$. The forgery comes after the last query.
>
> ---
> ### Experiment
> A search game with one branch; row 4 checks the winning conditions. `[BS §13.1.1]` `[GMR88 §2.2–2.3]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$ | $\xrightarrow{\ \mathrm{pk}\ }$ | |
> | 2 | | $\xleftarrow{\ m_i\ }$ | **Signing queries** (repeated, adaptive, at most $Q$ times): sends $m_i \in \mathcal M$ |
> | | $\sigma_i \leftarrow \mathsf{Sign}(\mathrm{sk}, m_i)$ | $\xrightarrow{\ \sigma_i\ }$ | |
> | 3 | | $\xleftarrow{\ m,\, \sigma\ }$ | outputs a candidate forgery $(m, \sigma)$ |
> | 4 | $b = \mathsf{Verify}(\mathrm{pk}, m, \sigma)$<br>checks whether $m \in \{m_1, m_2, \dots\}$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $b = 1$;
> - $m \notin \{m_1, m_2, \dots\}$: a signature on one new message suffices — an **existential forgery**.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathsf{SIG}}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $\mathsf{SIG}$ is **secure** — **existentially unforgeable under an adaptive chosen-message attack** (EUF-CMA) — if $\mathsf{Adv}^{\mathsf{euf\text{-}cma}}_{\mathsf{SIG}}(\mathcal A)$ is negligible for every efficient $\mathcal A$.
> - $\mathsf{SIG}$ is a **secure $q$-time signature** if this holds for every $\mathcal A$ that issues at most $q$ signing queries; for $q = 1$, a **secure one-time signature**.
>
> A *search* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Notation in the literature
> - `[BS §13.1.1]` writes the advantage $\text{SIGadv}[\mathcal A, \mathcal S]$ and the game as a list of steps.
> - `[AABN02 Def 2.2]` writes the forger as an oracle machine $F^{S_\mathrm{sk}(\cdot)}(\mathrm{pk})$ that outputs $(M, \sigma)$; the experiment returns $0$ when $M$ was queried. Here $\mathcal A$ is one stateful machine and each oracle call is a pair of rows, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!question] Security against multi-key attacks
> In real systems there are many users, each with a key pair $(\mathrm{pk}_i, \mathrm{sk}_i)$ for $i = 1, \dots, n$. Can a chosen-message attack on $\mathrm{pk}_1$ help the adversary forge signatures for $\mathrm{pk}_2$?

#### Random-oracle version

> [!definition] Parameters
> - The scheme $\mathsf{SIG}$ and the adversary $\mathcal A$ above.
> - $H$: a hash function that $\mathsf{Sign}$ and $\mathsf{Verify}$ call, modeled as a [[knowledge/cryptography/assumptions/idealized models/Random Oracle Model\|random oracle]] from $\mathcal X_H$ to $\mathcal Y_H$.
> - $Q_\mathrm{ro}$, $Q_\mathrm{s}$: bounds on the hash and signing queries.

> [!definition] Unforgeability in the Random Oracle Model
> The challenger also plays $H$: a random function $H \in \mathsf{Funs}[\mathcal X_H, \mathcal Y_H]$, evaluated on demand; hash and signing queries interleave as $\mathcal A$ chooses. `[BS §13.1.1]` `[AABN02 Def 2.2]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $H \xleftarrow{\$} \mathsf{Funs}[\mathcal X_H, \mathcal Y_H]$<br>$(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$ | $\xrightarrow{\ \mathrm{pk}\ }$ | |
> | 2 | | $\xleftarrow{\ x_j\ }$ | **Hash queries** (repeated, adaptive, at most $Q_\mathrm{ro}$ times): sends $x_j \in \mathcal X_H$ |
> | | $y_j \leftarrow H(x_j)$ | $\xrightarrow{\ y_j\ }$ | |
> | 3 | | $\xleftarrow{\ m_i\ }$ | **Signing queries** (repeated, adaptive, at most $Q_\mathrm{s}$ times): sends $m_i \in \mathcal M$ |
> | | $\sigma_i \leftarrow \mathsf{Sign}^H(\mathrm{sk}, m_i)$ | $\xrightarrow{\ \sigma_i\ }$ | |
> | 4 | | $\xleftarrow{\ m,\, \sigma\ }$ | outputs a candidate forgery $(m, \sigma)$ |
> | 5 | $b = \mathsf{Verify}^H(\mathrm{pk}, m, \sigma)$<br>checks whether $m \in \{m_1, m_2, \dots\}$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $b = 1$;
> - $m \notin \{m_1, m_2, \dots\}$.
>
> The advantage is $\mathsf{Adv}^{\mathsf{euf\text{-}cma\text{-}ro}}_{\mathsf{SIG}}(\mathcal A) = \Pr[\mathcal A \text{ wins}]$. The [[knowledge/cryptography/identification protocol/Schnorr Identification#Security Analysis of Schnorr Signatures\|Schnorr]] and [[knowledge/cryptography/primitive/digital signatures/ID and Signatures from Sigma#The Fiat-Shamir Heuristic for Signatures\|Fiat–Shamir]] signature theorems are stated for it.

### Strong Unforgeability

> [!definition] Parameters
> - As in [[knowledge/cryptography/primitive/digital signatures/Digital Signature#Unforgeability\|#Unforgeability]]: $\mathsf{SIG}$, $\mathcal A$, $Q$, the queries $m_i$ with their answers $\sigma_i$, and the candidate forgery $(m, \sigma)$.

> [!definition] Strong Unforgeability under Chosen-Message Attack
> ### Scope
> A signature scheme $\mathsf{SIG}$ and an efficient adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access**, **Promise**, **Quantifier**, **Adaptivity** — as in [[knowledge/cryptography/primitive/digital signatures/Digital Signature#Unforgeability\|#Unforgeability]].
>
> ---
> ### Experiment
> A search game with one branch; it differs from [[knowledge/cryptography/primitive/digital signatures/Digital Signature#Unforgeability\|#Unforgeability]] only in the freshness check of row 4. `[BS §13.1.1]` `[ADR02 §2.2]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$ | $\xrightarrow{\ \mathrm{pk}\ }$ | |
> | 2 | | $\xleftarrow{\ m_i\ }$ | **Signing queries** (repeated, adaptive, at most $Q$ times): sends $m_i \in \mathcal M$ |
> | | $\sigma_i \leftarrow \mathsf{Sign}(\mathrm{sk}, m_i)$ | $\xrightarrow{\ \sigma_i\ }$ | |
> | 3 | | $\xleftarrow{\ m,\, \sigma\ }$ | outputs a candidate forgery $(m, \sigma)$ |
> | 4 | $b = \mathsf{Verify}(\mathrm{pk}, m, \sigma)$<br>checks whether $(m, \sigma) \in \{(m_1, \sigma_1), (m_2, \sigma_2), \dots\}$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $b = 1$;
> - $(m, \sigma) \notin \{(m_1, \sigma_1), (m_2, \sigma_2), \dots\}$: a new signature on an already signed message counts.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{suf\text{-}cma}}_{\mathsf{SIG}}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $\mathsf{SIG}$ is **strongly unforgeable** (sUF-CMA) if $\mathsf{Adv}^{\mathsf{suf\text{-}cma}}_{\mathsf{SIG}}(\mathcal A)$ is negligible for every efficient $\mathcal A$; **strongly secure $q$-time** and **one-time** as above.
>
> Strong unforgeability implies unforgeability: a forgery on a new message is in particular a new pair.

> [!remark] Notation in the literature
> `[ADR02 §2.2]` calls this **strong unforgeability**, a notion that only makes sense under a chosen-message attack. `[BS §13.1.1]` calls it *strongly secure* and writes the advantage $\text{stSIGadv}[\mathcal A, \mathcal S]$.

## Related

### Instantiations

| | hardness | proof |
| --- | --- | --- |
| [[knowledge/cryptography/primitive/digital signatures/scheme/ElGamal Signature\|ElGamal Signature]] | discrete logarithm | none for the textbook scheme; a modified scheme in the random oracle model |
| [[knowledge/cryptography/primitive/digital signatures/Digital Signature Algorithm\|Digital Signature Algorithm]] | discrete logarithm | — |
| [[knowledge/cryptography/primitive/digital signatures/scheme/Lyubashevsky Signature\|Lyubashevsky Signature]] | SIS | random oracle model |
| [[knowledge/cryptography/primitive/digital signatures/scheme/Dilithium\|Dilithium]] | Module-LWE, Module-SIS | — |

### Constructions

| | from | gives |
| --- | --- | --- |
| [[knowledge/cryptography/primitive/digital signatures/Lamport Signature\|Lamport Signature]] | a one-way function | a one-time signature on $v$ bits |
| [[knowledge/cryptography/primitive/digital signatures/General Lamport Framework\|General Lamport Framework]] | a one-way function, a PRF, a containment-free $P$ | a one-time signature |
| [[knowledge/cryptography/primitive/digital signatures/Winternitz Signature\|Winternitz Signature]] | a function one-way on $d$ iterates, a PRG, a collision-resistant hash | a one-time signature with hash chains |
| [[knowledge/cryptography/primitive/digital signatures/Hash-and-Sign\|Hash-and-Sign]] | a signature and a collision-resistant hash | a signature on long messages |
| [[knowledge/cryptography/primitive/digital signatures/Hash-and-Sign with Target Collision Resistance\|Hash-and-Sign with Target Collision Resistance]] | a signature and a TCR hash | a signature on long messages, salted |
| [[knowledge/cryptography/primitive/digital signatures/Randomized Lamport Signature\|Randomized Lamport Signature]] | Lamport and an eTCR hash | a one-time signature on long messages |

- [[knowledge/cryptography/primitive/digital signatures/ID and Signatures from Sigma\|ID and Signatures from Sigma]], [[knowledge/cryptography/verifiable computing/compiler/Fiat-Shamir Transform\|Fiat-Shamir Transform]] — a Σ-protocol identification scheme becomes a signature in the random oracle model

### Siblings
- [[knowledge/cryptography/primitive/message authentication/Message Integrity\|Message Integrity]] — the symmetric analogue: one shared key signs and verifies, so a MAC cannot be checked by third parties
- [[knowledge/cryptography/primitive/digital signatures/Ring Signature\|Ring Signature]] — signed by some key of a ring, without saying which
- [[knowledge/cryptography/primitive/digital signatures/Blind Signature\|Blind Signature]] — the signer does not see what it signs
