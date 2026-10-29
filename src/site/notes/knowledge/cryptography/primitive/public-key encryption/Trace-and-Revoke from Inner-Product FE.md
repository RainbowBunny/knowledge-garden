---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/public-key-encryption/trace-and-revoke-from-inner-product-fe/","dg-note-properties":{"aliases":["ABPSY17 Trace-and-Revoke"]}}
---

Reference:
- `[ABPSY17]` — S. Agrawal, S. Bhattacherjee, D. H. Phan, D. Stehlé, S. Yamada, _Efficient Public Trace and Revoke from Standard Assumptions_, ACM CCS 2017. Numbers refer to the full version, ePrint 2017/650, §3 (the construction, Lemma 14, Theorems 15 and 16, Lemma 17, footnote 4): https://eprint.iacr.org/2017/650.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme\|Trace-and-Revoke Scheme]]: Import $(\lambda, t, r, \mathcal{ID}, \mathrm{pd}, p_\mathrm{id}, R, S, D)$.
> - [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption\|Inner-Product Functional Encryption]]: Import $(\ell, p)$, with $\ell = t + r + 1$.
> - $\mathcal M = \mathbb Z_p$: the message space.
> - $\mathbf x_\mathrm{id} \in \mathbb Z_p^\ell$: the random key vector of user $\mathrm{id}$.
> - $\mathbf v_R \in \mathbb Z_p^\ell \setminus \{\mathbf 0\}$: a vector orthogonal to the key vectors of the revoked users; $\mathbf v_{S_i} \in \mathbb Z_p^\ell$: the probe vectors of $\mathsf{Trace}$. Both are computed by a fixed deterministic linear-system solver, so every algorithm derives the same vectors from the same sets.
> - $c > 0$: the constant of [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme#Public Traceability\|useful decoders]]. $p_i$: the probability that $D$ decrypts probe $i$, and $\hat p_i$ its estimate.
>
> `[ABPSY17 §3]`

> [!definition] Building Blocks
> - $\mathcal{FE} = (\mathsf{FE.Setup}, \mathsf{FE.KeyGen}, \mathsf{FE.Enc}, \mathsf{FE.Dec})$: any [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption\|inner-product functional encryption]] scheme over $\mathbb Z_p$ (universally quantified).

> [!definition] Trace-and-Revoke from Inner-Product FE
> - $(\mathrm{pk}, \mathrm{msk}) \leftarrow \mathsf{Setup}(1^\lambda, 1^t, 1^r)$: (Randomized) Setup algorithm.
>     - **Input**: the security parameter, the coalition bound $t$ and the revocation bound $r$, in unary.
>     - **Output**: the public key $\mathrm{pk}$ and the master secret key $\mathrm{msk}$; the public directory $\mathrm{pd}$ starts empty.
>     - **Steps**:
>         1. Sets $\ell = t + r + 1$.
>         2. Runs $(\mathrm{pk}, \mathrm{msk}) \leftarrow \mathsf{FE.Setup}(1^\lambda, 1^\ell)$.
>         3. Returns $(\mathrm{pk}, \mathrm{msk})$.
> - $\mathrm{sk}_\mathrm{id} \leftarrow \mathsf{KeyGen}(\mathrm{msk}, \mathrm{id})$: (Randomized) Key-generation algorithm.
>     - **Input**: $\mathrm{msk}$ and an identity $\mathrm{id} \in \mathcal{ID}$.
>     - **Output**: the secret key $\mathrm{sk}_\mathrm{id}$; the public information $p_\mathrm{id} = (\mathrm{id}, \mathbf x_\mathrm{id})$ is appended to $\mathrm{pd}$.
>     - **Steps**:
>         1. Samples $\mathbf x_\mathrm{id} \xleftarrow{\$} \mathbb Z_p^\ell$.
>         2. Appends $p_\mathrm{id} = (\mathrm{id}, \mathbf x_\mathrm{id})$ to $\mathrm{pd}$.
>         3. Returns $\mathrm{sk}_\mathrm{id} \leftarrow \mathsf{FE.KeyGen}(\mathrm{msk}, \mathbf x_\mathrm{id})$.
> - $C \leftarrow \mathsf{Enc}(\mathrm{pd}, \mathrm{pk}, R, m)$: (Randomized) Encryption algorithm.
>     - **Input**: $\mathrm{pd}$, $\mathrm{pk}$, a revoked set $R$ with $\lvert R \rvert \leq r$, and a message $m \in \mathbb Z_p$.
>     - **Output**: a ciphertext $C = (C_1, C_2)$.
>     - **Steps**:
>         1. Computes $\mathbf v_R \in \mathbb Z_p^\ell \setminus \{\mathbf 0\}$ with $\langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle = 0$ for every $\mathrm{id} \in R$.
>         2. Sets $\mathbf y_R = m \cdot \mathbf v_R$.
>         3. Returns $C = (C_1, C_2) = (\mathsf{FE.Enc}(\mathrm{pk}, \mathbf y_R), R)$.
> - $m \leftarrow \mathsf{Dec}(\mathrm{pd}, \mathrm{sk}_\mathrm{id}, C)$: (Deterministic) Decryption algorithm.
>     - **Input**: $\mathrm{pd}$, the secret key of user $\mathrm{id}$, and a ciphertext $C$.
>     - **Output**: a message $m \in \mathbb Z_p$, or $\perp$ (abort).
>     - **Steps**:
>         1. Parses $C = (C_1, C_2)$ with $C_2 = R$.
>         2. If $\mathrm{id} \in R$, returns $\perp$.
>         3. Computes $\mathbf v_R$ as in $\mathsf{Enc}$.
>         4. Returns $m = \mathsf{FE.Dec}(\mathrm{sk}_\mathrm{id}, C_1) / \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$.
> - $\mathrm{id} / \perp \leftarrow \mathsf{Trace}(\mathrm{pd}, R, S, \mathcal O_D)$: (Randomized) Tracing algorithm.
>     - **Input**: $\mathrm{pd}$, a revoked set $R$ with $\lvert R \rvert \leq r$, a suspect set $S$ with $\lvert S \rvert \leq t$, and oracle access $\mathcal O_D$ to a pirate decoder.
>     - **Output**: an identity $\mathrm{id} \in S$, or $\perp$.
>     - **Steps**:
>         1. Finds $m, m' \in \mathbb Z_p$ for which $\big\lvert \Pr[\mathcal O_D(C, m) = 1] - \Pr[\mathcal O_D(C', m) = 1] \big\rvert \geq 1/(2\lambda^c)$, where $C \leftarrow \mathsf{Enc}(\mathrm{pd}, \mathrm{pk}, R, m)$ and $C' \leftarrow \mathsf{Enc}(\mathrm{pd}, \mathrm{pk}, R, m')$: tries random pairs and estimates both probabilities with Hoeffding's inequality (Lemma 14 below).
>         2. Sets $S_1 = \{\mathrm{id}_1, \mathrm{id}_2, \dots\} = S \setminus R$.
>         3. Computes $\mathbf v_R$ as in $\mathsf{Enc}$.
>         4. For $i = 1, 2, \dots$:
>             1. Chooses $\mathbf v_{S_i}$:
>                 - if $i = 1$: $\mathbf v_{S_1} = \mathbf 0$;
>                 - if $S_i = \emptyset$: $\mathbf v_{S_i} = (m' - m)\, \mathbf v_R$;
>                 - otherwise: a solution of $\langle \mathbf x_\mathrm{id}, \mathbf v_{S_i} \rangle = 0$ for every $\mathrm{id} \in S_i \cup R$, and $\langle \mathbf x_\mathrm{id}, \mathbf v_{S_i} \rangle = (m' - m) \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$ for every $\mathrm{id} \in S_1 \setminus S_i$.
>             2. Builds probes $C_{S_i} = \big(\mathsf{FE.Enc}(\mathrm{pk}, \mathbf v_{S_i} + m\, \mathbf v_R), R\big)$, queries $\mathcal O_D(C_{S_i}, m)$ repeatedly, and estimates $p_i$ by $\hat p_i$ (Hoeffding).
>             3. If $i > 1$ and $\lvert \hat p_i - \hat p_{i-1} \rvert$ is non-negligible, returns $\mathrm{id}_{i-1}$.
>             4. If $S_i = \emptyset$, returns $\perp$; otherwise sets $S_{i+1} = S_i \setminus \{\mathrm{id}_i\}$.
>
> `[ABPSY17 §3]`

> [!remark] Why the probes walk from $m$ to $m'$
> Probe $1$ encrypts $m\, \mathbf v_R$, an honest encryption of $m$; the last probe ($S_i = \emptyset$) encrypts $m'\, \mathbf v_R$, an honest encryption of $m'$. A user $\mathrm{id} \in S_1$ decrypts probe $i$ to $m$ while $\mathrm{id} \in S_i$ and to $m'$ once $\mathrm{id} \in S_1 \setminus S_i$; the probe vectors are not constrained on users outside $S \cup R$, which is why the suspect set must contain every traitor. By step 1 the end probabilities differ by at least $1/(2\lambda^c)$, so some consecutive pair $p_{i-1}, p_i$ differs noticeably, and among the users of $S \cup R$ the only key that tells probe $i - 1$ from probe $i$ is that of $\mathrm{id}_{i-1}$.

> [!remark] Notation in the source
> `[ABPSY17 Def 1]` gives $\mathsf{Enc}$ and $\mathsf{Dec}$ no $\mathrm{pd}$ argument and lets $\mathsf{KeyGen}$ output $(\mathrm{sk}_\mathrm{id}, p_\mathrm{id})$; the construction of §3 passes $\mathrm{pd}$ to both and has $\mathsf{KeyGen}$ append $p_\mathrm{id}$ to $\mathrm{pd}$, as above. The pirate decoder is assumed stateless (resettable): it answers each query independently of earlier ones `[ABPSY17 fn 4]`.

## Property

### Correctness

> [!proposition] Correctness — a non-revoked user recovers $m$
> For $\mathrm{id} \notin R$ with $\langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle \neq 0$, correctness of $\mathcal{FE}$ gives $\mathsf{FE.Dec}(\mathrm{sk}_\mathrm{id}, C_1) = \langle \mathbf x_\mathrm{id}, m\, \mathbf v_R \rangle = m \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$, so step 4 of $\mathsf{Dec}$ returns $m$. A revoked user has $\langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle = 0$ and learns $\mathsf{FE.Dec} = 0$, nothing about $m$.

## Security

> [!security] IND-CPA from $r$-IND-CPA `[ABPSY17 Thm 15]`
> If $\mathcal{FE}$ is $r$-IND-CPA secure ([[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption#Random-key bounded collusion\|random-key bounded collusion]], at most $r$ key queries), then the scheme is [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme#IND-CPA\|IND-CPA secure]].

> [!security] Public traceability from $(t + r)$-IND-CPA `[ABPSY17 Thm 16]`
> If $\mathcal{FE}$ is $(t + r)$-IND-CPA secure ([[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption#Random-key bounded collusion\|random-key bounded collusion]], at most $t + r$ key queries), then the scheme is [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme#Public Traceability\|publicly traceable]].

> [!lemma] Lemma 14 — a random message pair separates a useful decoder
> Let $R$ be arbitrary and assume $D$ is useful for $R$ (Equation (1) of [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme#Public Traceability\|Trace-and-Revoke Scheme#Public Traceability]]). Then with probability at least $1/(4\lambda^c)$ over $m, m' \xleftarrow{\$} \mathcal M$,
> $$\big\lvert \Pr[\mathcal O_D(C, m) = 1] - \Pr[\mathcal O_D(C', m) = 1] \big\rvert \geq \frac{1}{2\lambda^c},$$
> where $C \leftarrow \mathsf{Enc}(\mathrm{pk}, R, m)$ and $C' \leftarrow \mathsf{Enc}(\mathrm{pk}, R, m')$. `[ABPSY17 Lemma 14]`

> [!lemma] Lemma 17 — tracing a useful decoder does not give up
> If $D$ satisfies Equation (1), then with overwhelming probability $\mathsf{Trace}$ does not output $\perp$, and outputs some $\mathrm{id} \in S$. `[ABPSY17 Lemma 17]`

### Proof of Theorem 16

> [!proof] Reduction $\mathcal B$ `[ABPSY17, proof of Thm 16]`
> $\mathcal B$ plays the [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption#Random-key bounded collusion\|$(t + r)$-IND-CPA game]] against $\mathcal{FE}$ and simulates the [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme#Public Traceability\|$\mathsf{AD}\text{-}\mathsf{TT}$ game]] for $\mathcal A$; all three are stateful interactive machines.
>
> | | FE challenger $\mathcal C_\mathsf{FE}$ | | reduction $\mathcal B$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- | --- | --- |
> | 1 | $(\mathrm{pk}, \mathrm{msk}) \leftarrow \mathsf{FE.Setup}(1^\lambda, 1^\ell)$<br>$\ell = t + r + 1$ | $\xrightarrow{\ \mathrm{pk}\ }$ | $\mathrm{pd} \leftarrow \emptyset$<br>$T \leftarrow \emptyset$ | $\xrightarrow{\ \mathrm{pk}\ }$ | |
> | 2 | | | | $\xleftarrow{\ \mathrm{id}\ }$ | **Add users** (repeated, adaptive, polynomially many times): sends $\mathrm{id} \in \mathcal{ID}$ |
> | | | $\xleftarrow{\ \text{new vector}\ }$ | asks for a fresh random vector | | |
> | | $\mathbf x_\mathrm{id} \xleftarrow{\$} \mathbb Z_p^\ell$ | $\xrightarrow{\ \mathbf x_\mathrm{id}\ }$ | $p_\mathrm{id} = (\mathrm{id}, \mathbf x_\mathrm{id})$<br>$\mathrm{pd} \leftarrow \mathrm{pd} \cup \{p_\mathrm{id}\}$ | $\xrightarrow{\ \mathrm{pd}\ }$ | |
> | 3 | | | | $\xleftarrow{\ \mathrm{id}\ }$ | **Traitor key queries** (repeated, adaptive, at most $t$ times) |
> | | | $\xleftarrow{\ \mathbf x_\mathrm{id}\ }$ | if $\mathrm{id}$ is new, first runs row 2<br>makes a key query on $\mathbf x_\mathrm{id}$ | | |
> | | $\mathrm{sk}_{\mathbf x_\mathrm{id}} \leftarrow \mathsf{FE.KeyGen}(\mathrm{msk}, \mathbf x_\mathrm{id})$ | $\xrightarrow{\ \mathrm{sk}_{\mathbf x_\mathrm{id}}\ }$ | $T \leftarrow T \cup \{\mathrm{id}\}$ | $\xrightarrow{\ \mathrm{sk}_\mathrm{id}\ }$ | |
> | 4 | | | | $\xleftarrow{\ R\ }$ | **Revocation**: sends $R \subseteq \mathrm{pd}$ with $\lvert R \rvert \leq r$ |
> | | | $\xleftarrow{\ \{\mathbf x_\mathrm{id} \,:\, p_\mathrm{id} \in R\}\ }$ | $\lvert R \rvert$ key queries; at most $t + r$ in all | | |
> | | $\mathrm{sk}_{\mathbf x_\mathrm{id}} \leftarrow \mathsf{FE.KeyGen}(\mathrm{msk}, \mathbf x_\mathrm{id})$, for each | $\xrightarrow{\ \{\mathrm{sk}_{\mathbf x_\mathrm{id}}\}\ }$ | | $\xrightarrow{\ \{\mathrm{sk}_\mathrm{id} \,:\, p_\mathrm{id} \in R\}\ }$ | |
> | 5 | | | | $\xleftarrow{\ D,\, S\ }$ | outputs a pirate decoder $D$ and a suspect set $S \supseteq T$ with $\lvert S \rvert \leq t$ |
> | 6 | | | runs $\mathsf{Trace}(\mathrm{pd}, R, S, \mathcal O_D)$ itself — every input is public<br>obtains $m, m'$, $\mathbf v_R$, the $\mathbf v_{S_i}$, the estimates $\hat p_i$, and $\mathrm{out}$ | | |
> | 7 | | | **if** $\mathrm{out} = \perp$ **or** $\mathrm{out} = \mathrm{id}_{i-1} \in T$: outputs $b' \xleftarrow{\$} \{0, 1\}$ and stops | | |
> | 8 | | $\xleftarrow{\ \mathbf y_0,\, \mathbf y_1\ }$ | $\mathbf y_0 = \mathbf v_{S_{i-1}} + m\, \mathbf v_R$<br>$\mathbf y_1 = \mathbf v_{S_i} + m\, \mathbf v_R$ | | |
> | | **Game 0**: $\mathrm{ct}^* \leftarrow \mathsf{FE.Enc}(\mathrm{pk}, \mathbf y_0)$<br>**Game 1**: $\mathrm{ct}^* \leftarrow \mathsf{FE.Enc}(\mathrm{pk}, \mathbf y_1)$ | $\xrightarrow{\ \mathrm{ct}^*\ }$ | | | |
> | 9 | | | $\beta \leftarrow \mathcal O_D\big((\mathrm{ct}^*, R), m\big)$ — one more query to $D$ | | |
> | 10 | | $\xleftarrow{\ b'\ }$ | $b' = \beta$ if $\hat p_i > \hat p_{i-1}$<br>$b' = 1 - \beta$ otherwise | | |

> [!remark] Admissibility of the challenge (row 8) `[ABPSY17, proof of Thm 16]`
> Every key $\mathcal B$ queried belongs to $R \cup T$, and $T \subseteq S$. In row 8, $\mathrm{id}_{i-1} \notin T$.
>
> | key queried by $\mathcal B$ | $\langle \mathbf x_\mathrm{id}, \mathbf y_0 \rangle$ | $\langle \mathbf x_\mathrm{id}, \mathbf y_1 \rangle$ | equal? |
> | --- | --- | --- | --- |
> | $\mathrm{id} \in R$ | $0$ | $0$ | ✓ |
> | traitor in $S_{i-1}$, hence in $S_i$ since $\mathrm{id}_{i-1} \notin T$ | $m \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$ | $m \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$ | ✓ |
> | traitor in $S_1 \setminus S_{i-1}$ | $m' \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$ | $m' \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$ | ✓ |
> | $\mathrm{id}_{i-1}$ — never queried | $m \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$ | $m' \langle \mathbf x_\mathrm{id}, \mathbf v_R \rangle$ | ✗, allowed |
>
> A traitor outside $S$ would have an unconstrained $\langle \mathbf x_\mathrm{id}, \mathbf v_{S_i} \rangle$ and could make the challenge inadmissible: the proof uses $T \subseteq S$.

> [!proof] Advantage of $\mathcal B$
> Let $E$ be the event that $\mathcal B$ reaches row 8: $\mathsf{Trace}$ accuses $\mathrm{id}_{i-1} \notin T$. It is decided before the challenge, so it is the same in both games. On $E$, $(\mathrm{ct}^*, R)$ is distributed exactly as probe $i - 1$ (Game 0) or probe $i$ (Game 1), and $D$ answers independently of earlier queries `[ABPSY17 fn 4]`, so
> $$\Pr[\beta = 1 \mid \text{Game } b, E] = p_{i-1+b}.$$
> Off $E$, $b'$ is a uniform bit in both games. Hence, when the estimates order $p_{i-1}$ and $p_i$ correctly,
> $$\Pr[b' = 1 \mid \text{Game } 1] - \Pr[b' = 1 \mid \text{Game } 0] = \Pr[E] \cdot \lvert p_i - p_{i-1} \rvert.$$
> The source argues that both factors are non-negligible:
> - $\Pr[E]$: $\mathcal A$ wins $\mathsf{AD}\text{-}\mathsf{TT}$ with probability at least $1/\lambda^c$, that is $\mathrm{out} = \perp$ or $\mathrm{out} \notin T$, and by Lemma 17 $\mathrm{out} = \perp$ only with negligible probability;
> - $\lvert p_i - p_{i-1} \rvert$: $\mathsf{Trace}$ accuses only when $\lvert \hat p_i - \hat p_{i-1} \rvert$ is non-negligible, and by Hoeffding's inequality $\hat p_j$ is close to $p_j$, except with negligible probability.
>
> So $\mathcal B$ breaks the $(t + r)$-IND-CPA security of $\mathcal{FE}$. In the bit-guessing form of the source the advantage is half of this difference, $\Pr[E] \cdot \lvert p_i - p_{i-1} \rvert / 2$. $\blacksquare$

> [!remark] A slip in the source
> The proof in `[ABPSY17]` says that $\mathcal B$ outputs a random bit "if $\mathsf{Trace}$ outputs $\perp$ or index $i$ such that $\mathrm{id}_{i-1} \notin T$ but $\mathrm{id}_{i-1} \in S$", and two sentences later that, when it does not, "$\mathrm{id}_{i-1} \notin T$ but $\mathrm{id}_{i-1} \in S$". The admissibility argument needs $\mathrm{id}_{i-1} \notin T$ in the case where $\mathcal B$ continues, so the random-bit case is $\mathrm{id}_{i-1} \in T$, as in row 7.

## Related

### Instantiations
- [[knowledge/cryptography/primitive/functional encryption/scheme/Bounded-Collusion LWE Inner-Product FE\|Bounded-Collusion LWE Inner-Product FE]] — an $L$-IND-CPA scheme from LWE, built for this transform `[ABPSY17 §4.2]`
- DDH- and DCR-based instantiations `[ABPSY17 §5]`

### Prerequisites
- [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme\|Trace-and-Revoke Scheme]] — the output primitive and its two games
- [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption\|Inner-Product Functional Encryption]] — the input primitive and its random-key bounded-collusion game
