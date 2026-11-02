---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/block-cipher/block-ciphers/","dg-note-properties":{"aliases":["Block Cipher","Pseudorandom Permutation","PRP"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, Ch. 4: §4.1 (definition), §4.1.1 (implications of security), §4.1.3 (strongly secure block ciphers), §4.4.3 (block ciphers as PRFs), §4.7.2 (exhaustive search in the ideal cipher model): https://toc.cryptobook.us/ `⚠️ CLAUDE – verify:` only the table of contents of the book could be read; the games keep the wording of the previous version of this note.
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §7.2.1, Definition 7.1: https://cacr.uwaterloo.ca/hac/about/chap7.pdf
- `[Ros]` — M. Rosulek, _The Joy of Cryptography_, Ch. 7: Definition 7.1.2 (PRP), Lemma 7.2.1 (PRF–PRP switching), Definition 7.5.1 (strong PRP): https://joyofcryptography.com/prp/
- `[KL Def 3.28]` — J. Katz, Y. Lindell, _Introduction to Modern Cryptography_, 2nd ed., CRC Press, 2014, Definition 3.28 (strong pseudorandom permutation). The number is the one listed in https://www.cs.purdue.edu/homes/jblocki/courses/555_Spring21/slides/Week3.pdf; the definition itself was not read.
- `⚠️ CLAUDE – verify:` — a point I could not check against the source.

## Syntax

> [!definition] Parameters
> - $\mathcal K$: the key space; a key $k$ is sampled uniformly from it.
> - $\mathcal X$: the **data block space**, a finite set; its elements are **data blocks**.

> [!definition] Block Cipher
> A **block cipher** $\mathcal E = (E, D)$ defined over $(\mathcal K, \mathcal X)$ is a pair of efficient algorithms:
> - $y \leftarrow E(k, x)$: (Deterministic) Encryption algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a data block $x \in \mathcal X$.
>     - **Output**: a data block $y \in \mathcal X$.
> - $x \leftarrow D(k, y)$: (Deterministic) Decryption algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a data block $y \in \mathcal X$.
>     - **Output**: a data block $x \in \mathcal X$.
>
> It is a deterministic cipher whose message space and ciphertext space are the same set $\mathcal X$ `[BS §4.1]`: for each key, $E(k, \cdot)$ is a permutation of $\mathcal X$ and $D(k, \cdot)$ its inverse `[HAC Def 7.1]`.

> [!remark] Notation in the literature
> | source | algorithms | differences |
> | --- | --- | --- |
> | `[BS §4.1]` | $(E, D)$ over $(\mathcal K, \mathcal X)$ | no key generation: games sample $k \xleftarrow{R} \mathcal K$ |
> | `[HAC Def 7.1]` | $E(P, K)$ | the plaintext comes first; an $n$-bit block cipher has $\mathcal X = V_n = \{0, 1\}^n$ |
> | `[Ros Def 7.1.2]` | keyed permutation $F^\pm = (F, F^{-1})$ | security named PRP; the block length is a parameter |

## Property

### Correctness

> [!definition] Correctness
> For all $k \in \mathcal K$ and $x \in \mathcal X$,
> $$D(k, E(k, x)) = x.$$
> `[BS §4.1]`

## Security

### Secure Block Cipher

> [!definition] Parameters
> - The block cipher $\mathcal E = (E, D)$ over $(\mathcal K, \mathcal X)$ from Syntax.
> - $\mathrm{Perms}[\mathcal X]$: the set of all permutations of $\mathcal X$.
> - $\mathcal A$: an efficient [[knowledge/cryptography/foundations/Adversary\|Adversary]]; it is a **$Q$-query adversary** if it makes at most $Q$ queries.

> [!definition] Secure Block Cipher
> ### Scope
> A block cipher $\mathcal E$ and an efficient adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — forward queries only: $\mathcal A$ sends data blocks and receives their images under $E(k, \cdot)$ in Game 0, under a uniform permutation $f$ in Game 1.
> - **Promise** — none.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — each query may depend on the earlier answers.
>
> ---
> ### Experiment
> A distinguishing game: two branches, **Game 0** (the block cipher) and **Game 1** (a random permutation), that differ in rows 1 and 2. `[BS §4.1]` `[Ros Def 7.1.2]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | **Game 0**: $k \xleftarrow{\$} \mathcal K$<br>**Game 1**: $f \xleftarrow{\$} \mathrm{Perms}[\mathcal X]$ | | |
> | 2 | | $\xleftarrow{\ x_i\ }$ | **Queries** (repeated, adaptive): sends a data block $x_i \in \mathcal X$ |
> | | **Game 0**: $y_i \leftarrow E(k, x_i)$<br>**Game 1**: $y_i \leftarrow f(x_i)$ | $\xrightarrow{\ y_i\ }$ | |
> | 3 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{prp}}_{\mathcal E}(\mathcal A) = \Big|\Pr\big[\mathsf{Expt}_0(\mathcal A) = 1\big] - \Pr\big[\mathsf{Expt}_1(\mathcal A) = 1\big]\Big|.$$
> - $\mathcal E$ is **secure** — a **pseudorandom permutation** — if $\mathsf{Adv}^{\mathsf{prp}}_{\mathcal E}(\mathcal A)$ is negligible for every efficient $\mathcal A$.
>
> A *distinguishing* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Notation in the literature
> - `[BS §4.1]` lets the challenger select $f \in \mathrm{Perms}[\mathcal X]$ in both experiments — $f \leftarrow E(k, \cdot)$ in Experiment 0 — and answers every query with $f(x_i)$; rows 1 and 2 write the two cases out. Its advantage is $\text{BCadv}[\mathcal A, \mathcal E]$.
> - `[Ros Def 7.1.2]` states the same as the indistinguishability of two libraries, one answering with $F(k, \cdot)$, the other with a random permutation.
> - **Bit-guessing form** — the challenger picks $b$ at random and runs Game $b$; the bit-guessing advantage $|\Pr[b' = b] - 1/2|$ is half of $\mathsf{Adv}^{\mathsf{prp}}$ `[BS §4.1]`.

### Strongly Secure Block Cipher

> [!definition] Parameters
> - As in [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers#Secure Block Cipher\|#Secure Block Cipher]]; $f^{-1}$: the inverse of $f$.

> [!definition] Strongly Secure Block Cipher
> ### Scope
> A block cipher $\mathcal E$ and an efficient adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — forward queries, answered with $f(x_i)$, and inverse queries, answered with $f^{-1}(y_j)$, in any order; in Game 0 through $E(k, \cdot)$ and $D(k, \cdot)$.
> - **Promise** — none.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — each query may depend on the earlier answers.
>
> ---
> ### Experiment
> A distinguishing game: the game of [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Block Ciphers#Secure Block Cipher\|#Secure Block Cipher]] with inverse queries added; the branches differ in rows 1, 2 and 3. `[BS §4.1.3]` `[Ros Def 7.5.1]` `[KL Def 3.28]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | **Game 0**: $k \xleftarrow{\$} \mathcal K$<br>**Game 1**: $f \xleftarrow{\$} \mathrm{Perms}[\mathcal X]$ | | |
> | 2 | | $\xleftarrow{\ x_i\ }$ | **Forward queries** (repeated, adaptive): sends $x_i \in \mathcal X$ |
> | | **Game 0**: $y_i \leftarrow E(k, x_i)$<br>**Game 1**: $y_i \leftarrow f(x_i)$ | $\xrightarrow{\ y_i\ }$ | |
> | 3 | | $\xleftarrow{\ y_j\ }$ | **Inverse queries** (repeated, adaptive, interleaved with row 2): sends $y_j \in \mathcal X$ |
> | | **Game 0**: $x_j \leftarrow D(k, y_j)$<br>**Game 1**: $x_j \leftarrow f^{-1}(y_j)$ | $\xrightarrow{\ x_j\ }$ | |
> | 4 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{sprp}}_{\mathcal E}(\mathcal A) = \Big|\Pr\big[\mathsf{Expt}_0(\mathcal A) = 1\big] - \Pr\big[\mathsf{Expt}_1(\mathcal A) = 1\big]\Big|.$$
> - $\mathcal E$ is **strongly secure** — a **strong pseudorandom permutation** `[Ros Def 7.5.1]` `[KL Def 3.28]` — if $\mathsf{Adv}^{\mathsf{sprp}}_{\mathcal E}(\mathcal A)$ is negligible for every efficient $\mathcal A$.

### Unpredictability

> [!definition] Parameters
> - The block cipher $\mathcal E$ from Syntax. $Q$: the number of queries before the prediction.

> [!definition] Unpredictable Block Cipher
> ### Scope
> A block cipher $\mathcal E$ and an efficient adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — forward queries to $E(k, \cdot)$.
> - **Promise** — none.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — the queries and the final point may depend on the earlier answers.
>
> ---
> ### Experiment
> A search game: one branch. `[BS §4.1.1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $k \xleftarrow{\$} \mathcal K$ | | |
> | 2 | | $\xleftarrow{\ x_i\ }$ | **Queries** (repeated, adaptive, $Q$ times): sends $x_i \in \mathcal X$ |
> | | $y_i \leftarrow E(k, x_i)$ | $\xrightarrow{\ y_i\ }$ | |
> | 3 | | $\xleftarrow{\ x_{Q+1},\, y\ }$ | outputs a pair $(x_{Q+1}, y) \in \mathcal X^2$ |
> | 4 | $y^* \leftarrow E(k, x_{Q+1})$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $x_{Q+1} \notin \{x_1, \dots, x_Q\}$;
> - $y = y^*$.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{pred}}_{\mathcal E}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $\mathcal E$ is **unpredictable** if $\mathsf{Adv}^{\mathsf{pred}}_{\mathcal E}(\mathcal A)$ is negligible for every efficient $\mathcal A$.

### Key Recovery

> [!definition] Parameters
> - The block cipher $\mathcal E$ from Syntax.

> [!definition] Key Recovery
> ### Scope
> A block cipher $\mathcal E$ and an efficient adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — forward queries to $E(k, \cdot)$: chosen plaintexts.
> - **Promise** — none.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — each query may depend on the earlier answers.
>
> ---
> ### Experiment
> A search game: one branch. `[BS §4.1.1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $k \xleftarrow{\$} \mathcal K$ | | |
> | 2 | | $\xleftarrow{\ x_i\ }$ | **Queries** (repeated, adaptive): sends $x_i \in \mathcal X$ |
> | | $y_i \leftarrow E(k, x_i)$ | $\xrightarrow{\ y_i\ }$ | |
> | 3 | | $\xleftarrow{\ k'\ }$ | outputs a candidate key $k' \in \mathcal K$ |
> | 4 | compares $k'$ with $k$ | | |
>
> **Goal** — $\mathcal A$ wins iff:
> - $k' = k$.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{kr}}_{\mathcal E}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$
> - $\mathcal E$ is **secure against key recovery** if $\mathsf{Adv}^{\mathsf{kr}}_{\mathcal E}(\mathcal A)$ is negligible for every efficient $\mathcal A$.
> - In the [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|Ideal Cipher Model]] the advantage is written $\mathsf{Adv}^{\mathsf{kr\text{-}ic}}_{\mathcal E}(\mathcal A)$.

### Implications and a generic attack

> [!proposition] Secure, unpredictable, key-recovery secure — each notion implies the next
> **Scope**
> - $\mathcal E$: a block cipher over $(\mathcal K, \mathcal X)$.
>
> ---
> **Property**
> $$\text{secure} \implies \text{unpredictable} \implies \text{secure against key recovery}.$$
>
> `[BS §4.1.1]`. `⚠️ CLAUDE – verify:` the first implication needs $|\mathcal X|$ super-poly, since even a random permutation is predicted with probability $1/(|\mathcal X| - Q)$.

> [!proof] Why the second
> An adversary that recovers $k$ computes $E(k, x_{Q+1})$ for any new point and predicts it exactly.

> [!theorem] Exhaustive search in the ideal cipher model — enough plaintext–ciphertext pairs determine the key
> **Scope**
> - $\mathcal E$: a block cipher over $(\mathcal K, \mathcal X)$, modeled as an [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|ideal cipher]].
> - $Q$: the number of standard queries.
>
> ---
> **Property**
> There is a key-recovery adversary $\mathcal A_\mathrm{EX}$ making $Q$ standard queries and $Q |\mathcal K|$ ideal-cipher queries with
> $$\mathsf{Adv}^{\mathsf{kr\text{-}ic}}_{\mathcal E}(\mathcal A_\mathrm{EX}) \geq 1 - \varepsilon, \qquad \varepsilon = \frac{|\mathcal K|}{(|\mathcal X| - Q)^Q}.$$
>
> `[BS §4.7.2]`. $\mathcal A_\mathrm{EX}$ tries every key against the $Q$ pairs; $\varepsilon$ bounds the chance that a wrong key also fits them all.

> [!remark] A block cipher is a PRF `[BS §4.4.3]` `[Ros Lemma 7.2.1]`
> When $|\mathcal X|$ is super-poly, a secure block cipher is also a secure [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|PRF]] over $(\mathcal K, \mathcal X, \mathcal X)$: a random permutation and a random function are indistinguishable until a collision, which takes about $\sqrt{|\mathcal X|}$ queries.

## Related

### Instantiations

| | block | key | rounds | round |
| --- | --- | --- | --- | --- |
| [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Advanced Encryption Standard\|Advanced Encryption Standard]] | 128 bits | 128, 192 or 256 bits | 10, 12 or 14 | a substitution–permutation round: SubBytes, ShiftRows, MixColumns, AddRoundKey |
| [[knowledge/cryptography/primitive/symmetric encryption/block cipher/scheme/Data Encryption Standard\|Data Encryption Standard]] | 64 bits | 56 bits | 16 | a Feistel round |

### Constructions
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Iterated Block Cipher\|Iterated Block Cipher]] — a round cipher repeated with round keys from a key expansion; AES and DES
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Feistel Network\|Feistel Network]] — a permutation from any functions; with three rounds of a PRF, a secure block cipher (Luby–Rackoff)
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Substitution-Permutation Network\|Substitution-Permutation Network]] — rounds of key mixing, invertible S-boxes and a mixing permutation; AES
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Even-Mansour Cipher\|Even-Mansour Cipher]] — one public permutation and two whitening keys; EX and DESX
- [[knowledge/cryptography/primitive/symmetric encryption/block cipher/Multiple Encryption\|Multiple Encryption]] — double encryption (meet in the middle), triple encryption, Triple-DES
- [[knowledge/cryptography/primitive/symmetric encryption/Electronic Codebook Mode\|Electronic Codebook Mode]] — the block cipher applied to each block of a message
- [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function\|Davies-Meyer Compression Function]] — block cipher → compression function

### Properties
- [[knowledge/cryptography/assumptions/idealized models/Ideal Cipher Model\|Ideal Cipher Model]] — a random permutation for every key
- [[knowledge/cryptography/cryptanalysis/Linear Cryptanalysis\|Linear Cryptanalysis]] — a known-plaintext attack through a biased linear relation

### Siblings
- [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|Pseudorandom Function]] — no inverse; a secure block cipher on a large block space is one
- [[knowledge/cryptography/primitive/symmetric encryption/Stream Ciphers\|Stream Ciphers]], [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption\|Symmetric Key Encryption]] — a block cipher is a deterministic cipher; used alone it encrypts equal blocks equally
