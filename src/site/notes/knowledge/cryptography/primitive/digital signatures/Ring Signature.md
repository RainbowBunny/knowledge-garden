---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/ring-signature/","dg-note-properties":{}}
---

Reference:
- `[TNLPS26]` — N. Tran, K. Nguyen, D. Liu, J. Pieprzyk, W. Susilo, _Compact Lattice-Based NIZK Arguments for Set Membership and Ring Signatures without RO_, ePrint 2026/1885 (revision of an ASIACRYPT 2026 paper): abstract, §1 (Table 1), §2.3 (syntax, Definitions 4–6, following its references [7] and [29]): https://eprint.iacr.org/2026/1885

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter. $\mathrm{pp}$: public parameters, available to all users.
> - $(\mathrm{pk}, \mathrm{sk})$: a key pair. $M \in \{0, 1\}^*$: a message.
> - $R = (\mathrm{pk}_0, \dots, \mathrm{pk}_{N-1})$: a ring of public keys. $\Sigma$: a signature.
>
> `[TNLPS26 §2.3]`

> [!definition] Ring Signature Scheme
> A **ring signature scheme** is a tuple of PPT algorithms $(\mathsf{Setup}, \mathsf{KeyGen}, \mathsf{Sign}, \mathsf{Verify})$:
> - $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$: (Randomized) Setup algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: public parameters $\mathrm{pp}$.
> - $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm, run by each user.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: a key pair $(\mathrm{pk}, \mathrm{sk})$.
> - $\Sigma \leftarrow \mathsf{Sign}(\mathrm{sk}, M, R)$: (Randomized) Signing algorithm.
>     - **Input**: a secret key $\mathrm{sk}$, a message $M$, and a ring $R$; promise: $(\mathrm{pk}, \mathrm{sk})$ is a valid key pair and $\mathrm{pk} \in R$.
>     - **Output**: a signature $\Sigma$.
> - $b \leftarrow \mathsf{Verify}(M, R, \Sigma)$: (Deterministic) Verification algorithm.
>     - **Input**: a message, a ring and a signature.
>     - **Output**: $1$ (accept) or $0$ (reject).
>
> The signature shows that *some* member of $R$ signed, without saying which. `[TNLPS26 §2.3]`

> [!remark] Notation in the literature
> `[TNLPS26 §2.3]` writes $(\mathsf{RSetup}, \mathsf{RKeyGen}, \mathsf{RSign}, \mathsf{RVerify})$.

## Property

### Correctness

> [!definition] Correctness
> For all $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$, all $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$, all rings $R$ with $\mathrm{pk} \in R$ and all messages $M$,
> $$\mathsf{Verify}\big(M, R, \mathsf{Sign}(\mathrm{sk}, M, R)\big) = 1.$$
> `[TNLPS26 Def 4]`

## Security

### Unforgeability with respect to insider corruption

> [!definition] Parameters
> - The scheme's $\lambda, \mathrm{pp}$ from Syntax. $\mathcal A$: a PPT [[knowledge/cryptography/foundations/Adversary\|Adversary]].
> - $(\mathrm{pk}_j, \mathrm{sk}_j)$: the $j$-th key pair made by the challenger. $C$: the set of corrupted indices. $Q$: the signing queries made.

> [!definition] Unforgeability with Respect to Insider Corruption
> ### Scope
> A ring signature scheme and a PPT adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — three oracles: new honest keys, signatures by any honest key on any ring containing it, and corruption of any honest key.
> - **Promise** — none.
> - **Quantifier** — $\forall$ PPT $\mathcal A$.
> - **Adaptivity** — every query adaptive; the forgery's ring and message are chosen at the end.
>
> ---
> ### Experiment
> A search game with one branch. `[TNLPS26 Def 5]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$<br>$C \leftarrow \emptyset$<br>$Q \leftarrow \emptyset$ | $\xrightarrow{\ \mathrm{pp}\ }$ | |
> | 2 | | $\xleftarrow{\ \mathsf{PKGen}\ }$ | **Key generation** (repeated, adaptive): asks for a new key |
> | | $(\mathrm{pk}_j, \mathrm{sk}_j) \leftarrow \mathsf{KeyGen}(1^\lambda)$ for the next index $j$ | $\xrightarrow{\ \mathrm{pk}_j\ }$ | |
> | 3 | | $\xleftarrow{\ j,\, M,\, R\ }$ | **Signing** (repeated, adaptive) |
> | | if $\mathrm{pk}_j$ was generated in row 2 and $\mathrm{pk}_j \in R$:<br>$\Sigma \leftarrow \mathsf{Sign}(\mathrm{sk}_j, M, R)$<br>$Q \leftarrow Q \cup \{(M, R)\}$<br>else $\Sigma = \perp$ | $\xrightarrow{\ \Sigma\ }$ | |
> | 4 | | $\xleftarrow{\ j\ }$ | **Corruption** (repeated, adaptive) |
> | | if $\mathrm{pk}_j$ was generated in row 2: $C \leftarrow C \cup \{j\}$ | $\xrightarrow{\ \mathrm{sk}_j\ }$ | |
> | 5 | | $\xleftarrow{\ M^*,\, R^*,\, \Sigma^*\ }$ | outputs a forgery |
> | 6 | $b = \mathsf{Verify}(M^*, R^*, \Sigma^*)$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $b = 1$;
> - $(M^*, R^*) \notin Q$: no signing query was made on $(\cdot, M^*, R^*)$;
> - $R^*$ is nonempty;
> - every key in $R^*$ was generated in row 2 and none was corrupted.
>
> ---
> ### Property
> The scheme is **unforgeable with respect to insider corruption** if $\Pr[\mathcal A \text{ wins}]$ is negligible for every PPT $\mathcal A$.

### Anonymity against full key exposure

> [!definition] Parameters
> - The scheme's $\lambda, \mathrm{pp}$ from Syntax. $\mathcal A$: an [[knowledge/cryptography/foundations/Adversary\|Adversary]].
> - $N$: the number of honest keys. $r_i$: the random coins used to generate $(\mathrm{pk}_i, \mathrm{sk}_i)$.

> [!definition] Anonymity against Full Key Exposure
> ### Scope
> A ring signature scheme and an adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — the honest public keys, a signing oracle as in the unforgeability game, and, with the challenge, the key-generation coins of every honest key.
> - **Promise** — $\mathrm{pk}_{j_0}, \mathrm{pk}_{j_1} \in R^*$.
> - **Quantifier** — $\forall \mathcal A$ in the class considered (`[TNLPS26]`'s scheme achieves it statistically).
> - **Adaptivity** — $(M^*, j_0, j_1, R^*)$ chosen adaptively. One challenge.
>
> ---
> ### Experiment
> A distinguishing game: the branches differ in which of the two keys signs. `[TNLPS26 Def 6]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$<br>$(\mathrm{pk}_i, \mathrm{sk}_i) \leftarrow \mathsf{KeyGen}(1^\lambda; r_i)$ for $i \in [N]$, fresh coins $r_i$ | $\xrightarrow{\ \mathrm{pp},\, \{\mathrm{pk}_i\}\ }$ | |
> | 2 | | $\xleftarrow{\ i,\, M,\, R\ }$ | **Signing** (repeated, adaptive) |
> | | $\Sigma \leftarrow \mathsf{Sign}(\mathrm{sk}_i, M, R)$ if $\mathrm{pk}_i \in R$, else $\perp$ | $\xrightarrow{\ \Sigma\ }$ | |
> | 3 | | $\xleftarrow{\ M^*,\, j_0,\, j_1,\, R^*\ }$ | chooses a message, two indices and a ring containing both keys |
> | 4 | **Game 0**: $\Sigma^* \leftarrow \mathsf{Sign}(\mathrm{sk}_{j_0}, M^*, R^*)$<br>**Game 1**: $\Sigma^* \leftarrow \mathsf{Sign}(\mathrm{sk}_{j_1}, M^*, R^*)$ | $\xrightarrow{\ \Sigma^*,\, \{r_i\}_{i \in [N]}\ }$ | |
> | 5 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> The scheme is **anonymous against full key exposure** if this difference is negligible. With the coins $\{r_i\}$, $\mathcal A$ can recompute every secret key, so anonymity holds even when all keys are exposed. `[TNLPS26 Def 6]`

> [!remark] The source's form
> `[TNLPS26 Def 6]` samples $b$, signs with $\mathrm{sk}_{j_b}$ and asks for $\Pr[b' = b] = 1/2 + \mathrm{negl}(\lambda)$, writing the adversary as $\mathcal A^{\mathsf{Sign}(\cdot)}$; the difference above is twice the source's bias ([[knowledge/cryptography/primitive/public-key encryption/property/Indistinguishability under Chosen-Plaintext Attack#Bit-guessing form\|Indistinguishability under Chosen-Plaintext Attack#Bit-guessing form]]).

## Related

### Instantiations

| scheme | model | signature size |
| --- | --- | --- |
| Brakerski–Kalai, from ring trapdoor functions | plain | $\Omega(R \cdot \lambda \log \lambda)$ |
| Chatterjee et al. (CRYPTO 2021), from LWE | plain | $\Omega(\log R \cdot \lambda^4)$ |
| `[TNLPS26 §5]`, from a set-membership NIZK | CRS | $O(\log R \cdot \lambda^2 \log^2 \lambda)$ |

`[TNLPS26 §1, Table 1]`. The last is statistically anonymous and unforgeable under Module-LWE and Module-SIS `[TNLPS26 abstract]`.

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]] — a ring of one key
- [[knowledge/cryptography/primitive/digital signatures/Blind Signature\|Blind Signature]] — another signature that hides information from a party

### Constructions
- [[knowledge/cryptography/verifiable computing/relation/Set Membership Relation\|Set Membership Relation]] — a ring signature proves that the signer's key is in the ring
