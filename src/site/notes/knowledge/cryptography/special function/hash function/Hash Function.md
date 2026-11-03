---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/hash-function/","dg-note-properties":{"aliases":["Collision-Resistant Hash Function","CRHF"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§7.1 and §7.1.2: keyed hash functions; §8.1 and §8.1.1: collision resistance, Definition 8.1).
- `[HK06]` — S. Halevi, H. Krawczyk, _Strengthening Digital Signatures via Randomized Hashing_, CRYPTO 2006: Introduction, §3 (TCR), §4 (eTCR): https://www.iacr.org/archive/crypto2006/41170039/41170039.pdf
- `[HPS]` — J. Hoffstein, J. Pipher, J. H. Silverman, _An Introduction to Mathematical Cryptography_, 2nd ed., Springer, 2014, §8.1. `⚠️ CLAUDE – verify:` the informal description in Syntax follows this section's wording; the book could not be read.
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Syntax

> [!definition] Parameters
> - $\mathcal M$: the message space. 
> - $\mathcal T$: the digest space.
> - $\mathcal K$: the key space, for a keyed hash function.

> [!definition] Hash Function
> A **(keyless) hash function** $H$ defined over $(\mathcal M, \mathcal T)$ is one efficient algorithm:
> - $t \leftarrow H(m)$: (Deterministic) Hash algorithm.
>     - **Input**: a message $m \in \mathcal M$.
>     - **Output**: a **digest** $t \in \mathcal T$.
>
> `[BS §8.1]`

> [!remark] What a hash function is for `[HPS §8.1]`
> It maps an arbitrarily long document to a short digest, and it should be
> - fast to compute;
> - hard to invert: given a digest $t$, hard to find any $m$ with $H(m) = t$ — [[knowledge/cryptography/special function/one-way function/One-Way Functions\|one-wayness]];
> - collision resistant: hard to find $m_0 \neq m_1$ with $H(m_0) = H(m_1)$ — the game in Security.
>
> When $|\mathcal M| > |\mathcal T|$, collisions exist by the pigeonhole principle; the requirement is only that they be hard to find.

> [!remark] Asymptotic form `[BS §8.1.1]`
> With a system parameterization $P$, the spaces are families $M = \{\mathcal M_{\lambda, \Lambda}\}_{\lambda, \Lambda}$ and $T = \{\mathcal T_{\lambda, \Lambda}\}_{\lambda, \Lambda}$, both efficiently recognizable, and $H$ takes
> - $\lambda \in \mathbb Z_{\geq 1}$: the security parameter;
> - $\Lambda \in \mathrm{Supp}(P(\lambda))$: the system parameter;
> - $m \in \mathcal M_{\lambda, \Lambda}$: the message;
>
> and outputs an element of $\mathcal T_{\lambda, \Lambda}$. A family indexed by a public random matrix, such as [[knowledge/cryptography/special function/hash function/scheme/Ajtai Hash Function\|Ajtai Hash Function]] ($f_\mathbf A$), fits this form with the matrix inside $\Lambda$.

### Keyed hash function

> [!definition] Keyed Hash Function
> A **keyed hash function** $H$ defined over $(\mathcal K, \mathcal M, \mathcal T)$ is one efficient algorithm:
> - $t \leftarrow H(k, m)$: (Deterministic) Hash algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a message $m \in \mathcal M$.
>     - **Output**: a digest $t \in \mathcal T$.
>
> `[BS §7.1]`

> [!definition] Collision under a Key
> Messages $m_0, m_1 \in \mathcal M$ form a **collision for $H$ under the key $k \in \mathcal K$** iff
> - $H(k, m_0) = H(k, m_1)$;
> - $m_0 \neq m_1$.
>
> `[BS §7.1]`

> [!remark] Asymptotic form `[BS §7.1.2]`
> As for the keyless form, with three families $K, M, T$: all efficiently recognizable, and $K$ and $T$ also efficiently sampleable. $H$ takes $\lambda$, $\Lambda$, a key $k \in \mathcal K_{\lambda, \Lambda}$ and a message $m \in \mathcal M_{\lambda, \Lambda}$, and outputs an element of $\mathcal T_{\lambda, \Lambda}$.

## Security

### Collision Resistance

Specializes [[knowledge/cryptography/special function/Special Functions#Collision Resistant\|Special Functions#Collision Resistant]].

> [!definition] Parameters
> - $H$: a keyless hash function defined over $(\mathcal M, \mathcal T)$.
> - $\mathbb A$: the class of efficient [[knowledge/cryptography/foundations/Adversary\|adversaries]], each a **collision finder** when it plays this game.

> [!definition] Collision Resistance
> ### Scope
> A hash function $H$ defined over $(\mathcal M, \mathcal T)$ and the adversary class $\mathbb A$ of Parameters.
>
> ---
> ### Condition
> - **Access** — none: there is no key and no oracle, and $\mathcal A$ evaluates $H$ by itself.
> - **Promise** — none.
> - **Quantifier** — $\forall \mathcal A \in \mathbb A$.
> - **Adaptivity** — none: $\mathcal A$ speaks once.
>
> ---
> ### Experiment
> A search game: one branch, and the challenger checks the output in the last row. `[BS §8.1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | | $\xleftarrow{\ m_0,\, m_1\ }$ | outputs two messages $m_0, m_1 \in \mathcal M$ |
> | 2 | checks whether $m_0 \neq m_1$<br>checks whether $H(m_0) = H(m_1)$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $m_0 \neq m_1$;
> - $H(m_0) = H(m_1)$.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{cr}}_{H}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $H$ is **collision resistant** if $\mathsf{Adv}^{\mathsf{cr}}_{H}(\mathcal A)$ is negligible for every $\mathcal A \in \mathbb A$ `[BS Def 8.1]`.
>
> It is a *search* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Notation in the literature
> `[BS §8.1]` says that $\mathcal A$ *takes no input* and outputs $m_0, m_1$, and that $\mathcal A$ wins if the pair is a collision for $H$; here the adversary never has inputs, so row 1 is all there is. In the asymptotic form, $H$ also depends on the system parameter $\Lambda$.

> [!remark] In an idealized model
> When $H$ is built from a block cipher or a permutation modeled as ideal, $\mathcal A$ also gets oracle access to it, and the advantage is written $\mathsf{Adv}^{\mathsf{cr\text{-}ic}}_{H}(\mathcal A)$ — see [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function#Security\|Davies-Meyer Compression Function#Security]] and [[knowledge/cryptography/special function/hash function/Sponge Construction#Security\|Sponge Construction#Security]].

### Target Collision Resistance

> [!definition] Parameters
> - $H$: a keyed hash function defined over $(\mathcal K, \mathcal M, \mathcal T)$.
> - $r \in \mathcal K$: the key, a public random **salt**.
> - $\mathcal A$: an efficient [[knowledge/cryptography/foundations/Adversary\|Adversary]].

> [!definition] Target Collision Resistance
> ### Scope
> A keyed hash function $H$ and an efficient adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — none; $\mathcal A$ evaluates $H$ itself once it has the salt.
> - **Promise** — none.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — $\mathcal A$ commits to its first message before it sees the salt.
>
> ---
> ### Experiment
> A search game: one branch. `[HK06 §3]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | | $\xleftarrow{\ m_0\ }$ | commits to a first message $m_0 \in \mathcal M$ |
> | 2 | $r \xleftarrow{\$} \mathcal K$ | $\xrightarrow{\ r\ }$ | |
> | 3 | | $\xleftarrow{\ m_1\ }$ | outputs a second message $m_1 \in \mathcal M$ |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $m_1 \neq m_0$;
> - $H(r, m_1) = H(r, m_0)$.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{tcr}}_{H}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $H$ is **target collision resistant** (TCR) if $\mathsf{Adv}^{\mathsf{tcr}}_{H}(\mathcal A)$ is negligible for every efficient $\mathcal A$.

### Enhanced Target Collision Resistance

> [!definition] Parameters
> - As in [[knowledge/cryptography/special function/hash function/Hash Function#Target Collision Resistance\|#Target Collision Resistance]].

> [!definition] Enhanced Target Collision Resistance
> The game of [[knowledge/cryptography/special function/hash function/Hash Function#Target Collision Resistance\|#Target Collision Resistance]], except that in row 3 $\mathcal A$ outputs a second message **and a second salt** $(m_1, r')$, and wins iff all of:
> - $(m_1, r') \neq (m_0, r)$;
> - $H(r', m_1) = H(r, m_0)$.
>
> The advantage is $\mathsf{Adv}^{\mathsf{etcr}}_{H}(\mathcal A)$; $H$ is **enhanced TCR** (eTCR) if it is negligible for every efficient $\mathcal A$ `[HK06 Introduction, §4]`.

> [!remark] Why the enhancement
> A signature on $(r, H(r, m))$ needs only TCR; a signature on $H(r, m)$ alone, with $r$ sent in the clear, lets a forger change the salt too, which is what eTCR rules out `[HK06 Introduction, §1.1]` — [[knowledge/cryptography/primitive/digital signatures/Hash-and-Sign with Target Collision Resistance\|Hash-and-Sign with Target Collision Resistance]], [[knowledge/cryptography/primitive/digital signatures/Randomized Lamport Signature\|Randomized Lamport Signature]].

## Related

### Instantiations

| | built from | collision resistance rests on |
| --- | --- | --- |
| [[knowledge/cryptography/special function/hash function/scheme/Secure Hash Algorithm 256\|Secure Hash Algorithm 256]] | [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle–Damgård]] over [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function\|Davies–Meyer]] on the SHACAL-2 cipher | heuristic: the cipher treated as an ideal cipher |
| [[knowledge/cryptography/special function/hash function/scheme/Keccak\|Keccak]] | a [[knowledge/cryptography/special function/hash function/Sponge Construction\|sponge]] on Keccak-$f$ | heuristic: the permutation treated as random |
| [[knowledge/cryptography/special function/hash function/scheme/Message-Digest Algorithm 5\|Message-Digest Algorithm 5]] | Merkle–Damgård | broken: collisions found in 2004 |
| [[knowledge/cryptography/special function/hash function/scheme/Ajtai Hash Function\|Ajtai Hash Function]] | one random matrix over $\mathbb Z_q$ | [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|SIS]] |

### Constructions
- [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle-Damgard Transform]] — collision-resistant compression function → hash function on long messages
- [[knowledge/cryptography/special function/hash function/Sponge Construction\|Sponge Construction]] — permutation → hash function, in the ideal permutation model
- [[knowledge/cryptography/special function/compression function/Compression Functions\|Compression Functions]] — the fixed-length case, the building block of Merkle–Damgård

### Siblings
- [[knowledge/cryptography/special function/hash function/Universal Hash Function\|Universal Hash Function]] — keyed, the key kept secret, and the adversary never sees a digest: a weaker, often statistical guarantee
- [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|Pseudorandom Function]] — keyed with a secret key, and its outputs look random, not only collision-free
- [[knowledge/cryptography/special function/one-way function/One-Way Functions\|One-Way Functions]] — only preimages need to be hard to find
