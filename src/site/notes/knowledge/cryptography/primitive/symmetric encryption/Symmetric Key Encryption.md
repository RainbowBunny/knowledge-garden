---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/symmetric-key-encryption/","dg-note-properties":{}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (Ch. 2: Definition 2.1, Theorem 2.5, Attack Games 2.1–2.4, Definition 2.2; Ch. 5: Attack Games 5.1–5.3; Ch. 9: Attack Game 9.2). Definition 2.1, Theorem 2.5, Attack Game 2.1 and Definition 2.2 were checked in the book. `⚠️ CLAUDE – verify:` WebFetch returns only the first ~17 pages of the book, so Attack Games 2.2–2.4, 5.1–5.3 and 9.2 could not be read: their tables redraw the wording this note already had, and their numbers are those of the index in [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Encryption MOC\|Symmetric Encryption MOC]].
- `[KL]` — J. Katz, Y. Lindell, _Introduction to Modern Cryptography_, 2nd ed., CRC Press, 2014: §3.2 ($\mathsf{PrivK}^{\mathsf{eav}}$), §3.4 ($\mathsf{PrivK}^{\mathsf{cpa}}$), Definition 3.33 ($\mathsf{PrivK}^{\mathsf{cca}}$). Read through lecture slides that follow the book: https://user.eng.umd.edu/~danadach/Intro_Crypto_Spring_18/lec_8_18.pdf (eav and cpa) and https://www.cs.purdue.edu/homes/jblocki/courses/555_Spring21/slides/Week3.pdf (Definition 3.33).
- `⚠️ CLAUDE – verify:` — a point I could not check against the source.

## Syntax

> [!definition] Symmetric Key Encryption Scheme
> A **symmetric-key encryption scheme** $\text{SKE} = (\mathsf{KeyGen}, \text{Enc}, \text{Dec})$ is a triple of efficient algorithms with a message space $\mathcal M$, ciphertext space $\mathcal C$, randomness space $\mathcal R$ and key space $\mathcal K$.
> - $k \leftarrow \mathsf{KeyGen}()$: The key-generation algorithm $\mathsf{KeyGen}$ returns a key $k \in \mathcal K$ (often simply $k \xleftarrow{\$} \mathcal K$).
> - $c \leftarrow \text{Enc}(k, m)$ (Deterministic) or $c \leftarrow \text{Enc}(k, m; r)$ (Probabilistic): The encryption algorithm takes a key $k \in \mathcal K$, a message $m \in \mathcal M$ and possibly an internal random $r \leftarrow \mathcal R$ to produce a ciphertext $c \in \mathcal C$.
> - $m \leftarrow \text{Dec}(k, c)$: The deterministic decryption algorithm takes a key $k \in \mathcal K$ and a ciphertext $c$, and outputs either a message $m \in \mathcal M$ or a special symbol $\perp$ to indicate **rejection**.

> [!remark] Notation in the literature
> - `[KL]` writes $\Pi = (\mathsf{Gen}, \mathsf{Enc}, \mathsf{Dec})$ with $\mathsf{Gen}(1^n)$; here the security parameter is left implicit.
> - `[BS]` writes a **cipher** $\mathcal E = (E, D)$ defined over $(\mathcal K, \mathcal M, \mathcal C)$ and has no key-generation algorithm: its games pick $k \xleftarrow{R} \mathcal K$. A cipher is the case where $\mathsf{KeyGen}$ samples $k \xleftarrow{\$} \mathcal K$, and the games below taken from `[BS]` write that sampling.
> - The vault calls key generation $\mathsf{KeyGen}$ whatever the source writes ([[Note Layouts\|Note Layouts]] § *Game form*).

## Property

### Correctness

> [!definition] Correctness
> A symmetric cipher $\mathcal E = (E, D)$ is **correct** if for all keys $k \in \mathcal K$ and all messages $m \in \mathcal M$: $$D(k, E(k, m)) = m.$$

### Min-Entropy

> [!definition] Min-Entropy
> Given $k \in \mathcal K, m \in \mathcal M$, we define the **min-entropy** of $\text{Enc}(k, m)$ by
> $$\gamma(k, m) = -\log \max_{c \in \mathcal C} \Pr[c = \text{Enc}(k, m; r) \; | \; r \leftarrow \mathcal R].$$
> We say that a $\text{SKE}$ is $\gamma$**-spread** if:
> $$\forall k \in \mathcal K, m \in \mathcal M: \gamma(k, m) \geq \gamma$$

> [!remark]
> Equivalent formulation ($\gamma$-uniformity): $\mathcal E$ is $\gamma$-uniform if $\Pr[c = E(k, m; r) \;|\; r \in \mathcal R] \leq \gamma$ for all $k, m, c$. A $\gamma$-spread scheme is $2^{-\gamma}$-uniform (Hofheinz–Hövelmanns–Kiltz 2017). This matches the [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme (Old)#Min-Entropy\|PKE min-entropy]] definition.

## Security

### Perfect Security

> [!definition] Perfect Security `[BS Def 2.1]`
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. Consider a probabilistic experiment in which the random variable $K$ is uniformly distributed over $\mathcal K$. If for all $m_0, m_1 \in \mathcal M$ and all $c \in \mathcal C$: $$P[E(K, m_0) = c] = P[E(K, m_1) = c],$$ then $\mathcal E$ is **perfectly secure**.

> [!theorem] Shannon's Theorem `[BS Thm 2.5]`
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. If $\mathcal E$ is perfectly secure, then $|\mathcal K| \geq |\mathcal M|$.

> [!theorem] Generalized Shannon's Theorem
> Let $\mathcal E$ be a cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. Suppose the semantic security advantage $\text{SSadv}[\mathcal A, \mathcal E] \leq \epsilon$ for all adversaries $\mathcal A$, including **computationally unbounded** ones. Then $|\mathcal K| \geq (1 - \epsilon) |\mathcal M|$.

> [!remark]
> The equivalent characterizations (counting form, predicate form, independence form) are collected in [[knowledge/cryptography/primitive/symmetric encryption/Perfect Security\|Perfect Security]]. The canonical perfectly secure cipher is the [[knowledge/cryptography/primitive/symmetric encryption/classical/One-time Pad\|One-time Pad]].

### Indistinguishability

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Syntax\|SKE]] $= (\mathsf{KeyGen}, \mathsf{Enc}, \mathsf{Dec})$ with spaces $(\mathcal K, \mathcal M, \mathcal C, \mathcal R)$.
> - $\mathsf{atk} \in \{\mathsf{eav}, \mathsf{cpa}, \mathsf{cca}\}$: the attack; it fixes which queries are allowed.
> - $\mathbb A$: the class of efficient [[knowledge/cryptography/foundations/Adversary\|adversaries]]. $t$: the running-time bound. $\varepsilon$: the advantage bound.

> [!definition] SKE Indistinguishability (IND-ATK)
> ### Scope
> A symmetric-key encryption scheme $\text{SKE} = (\mathsf{KeyGen}, \mathsf{Enc}, \mathsf{Dec})$ and the adversary class $\mathbb A$ of Parameters.
>
> ---
> ### Condition
> - **Access** — there is no public key, so $\mathcal A$ sees encryptions only through the challenger; $\mathsf{atk}$ fixes which queries it may make:
>     - $\mathsf{eav}$ (eavesdropping attack): no query — rows 2, 3, 6 and 7 are skipped.
>     - $\mathsf{cpa}$ (chosen-plaintext attack): encryption queries before and after the challenge — rows 2 and 6.
>     - $\mathsf{cca}$ (chosen-ciphertext attack): encryption and decryption queries before and after the challenge — rows 2, 3, 6 and 7 — except a decryption query on $c^*$.
> - **Promise** — the two challenge messages have equal length, $|m_0| = |m_1|$.
> - **Quantifier** — $\forall \mathcal A \in \mathbb A$ of running time at most $t$.
> - **Adaptivity** — the queries and the choice of $m_0, m_1$ are adaptive; the queries of rows 2–3, and those of rows 6–7, may be interleaved in any order. One challenge.
>
> ---
> ### Experiment
> A distinguishing game: two branches that differ in row 5 only, **Game 0** and **Game 1**. `[KL §3.2]` ($\mathsf{eav}$), `[KL §3.4]` ($\mathsf{cpa}$), `[KL Def 3.33]` ($\mathsf{cca}$); the case $\mathsf{atk} = \mathsf{eav}$ is `[BS Attack Game 2.1]`.
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $k \leftarrow \mathsf{KeyGen}()$ | | |
> | 2 | | $\xleftarrow{\ m_i\ }$ | **Encryption queries** (repeated, adaptive; $\mathsf{cpa}$ and $\mathsf{cca}$ only): sends $m_i \in \mathcal M$ |
> | | $c_i \leftarrow \mathsf{Enc}(k, m_i)$ | $\xrightarrow{\ c_i\ }$ | |
> | 3 | | $\xleftarrow{\ \hat c_j\ }$ | **Decryption queries** (repeated, adaptive; $\mathsf{cca}$ only): sends $\hat c_j \in \mathcal C$ |
> | | $\hat m_j \leftarrow \mathsf{Dec}(k, \hat c_j)$ | $\xrightarrow{\ \hat m_j\ }$ | |
> | 4 | | $\xleftarrow{\ m_0,\, m_1\ }$ | chooses $m_0, m_1 \in \mathcal M$ with $\lvert m_0 \rvert = \lvert m_1 \rvert$ |
> | 5 | **Game 0**: $c^* \leftarrow \mathsf{Enc}(k, m_0)$<br>**Game 1**: $c^* \leftarrow \mathsf{Enc}(k, m_1)$ | $\xrightarrow{\ c^*\ }$ | |
> | 6 | | $\xleftarrow{\ m_i\ }$ | **Encryption queries** (repeated, adaptive; $\mathsf{cpa}$ and $\mathsf{cca}$ only): sends $m_i \in \mathcal M$ |
> | | $c_i \leftarrow \mathsf{Enc}(k, m_i)$ | $\xrightarrow{\ c_i\ }$ | |
> | 7 | | $\xleftarrow{\ \hat c_j\ }$ | **Decryption queries** (repeated, adaptive; $\mathsf{cca}$ only): sends $\hat c_j \in \mathcal C$ with $\hat c_j \neq c^*$ |
> | | $\hat m_j \leftarrow \mathsf{Dec}(k, \hat c_j)$ | $\xrightarrow{\ \hat m_j\ }$ | |
> | 8 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}^{\mathsf{ind}\text{-}\mathsf{atk}}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}^{\mathsf{ind}\text{-}\mathsf{atk}}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}^{\mathsf{ind}\text{-}\mathsf{atk}}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\text{Adv}_\text{SKE}^{\text{ind-atk}}(\mathcal A) = \Big|\Pr\big[\mathsf{Expt}^{\mathsf{ind}\text{-}\mathsf{atk}}_0(\mathcal A) = 1\big] - \Pr\big[\mathsf{Expt}^{\mathsf{ind}\text{-}\mathsf{atk}}_1(\mathcal A) = 1\big]\Big|.$$
> - **$(t,\varepsilon)$-IND-ATK security** — a SKE scheme is $(t, \varepsilon)$-IND-ATK secure if $\text{Adv}_\text{SKE}^{\text{ind-atk}}(\mathcal A) \leq \varepsilon$ for every adversary $\mathcal A$ with running time at most $t$.
> - A SKE scheme is **IND-ATK secure** if the advantage is negligible for every efficient $\mathcal A$ `[KL]`.
> - With $\mathsf{atk} = \mathsf{eav}$ and a $\mathsf{KeyGen}$ that samples $k \xleftarrow{\$} \mathcal K$, the advantage is $\text{SSadv}[\mathcal A, \mathcal E]$ of `[BS Attack Game 2.1]`, and IND-EAV security is **semantic security** `[BS Def 2.2]`.
>
> It is a *distinguishing* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Notation in the literature
> - `[KL]` calls the three experiments $\mathsf{PrivK}^{\mathsf{eav}}_{\mathcal A, \Pi}(n)$, $\mathsf{PrivK}^{\mathsf{cpa}}_{\mathcal A, \Pi}(n)$ and $\mathsf{PrivK}^{\mathsf{cca}}_{\mathcal A, \Pi}(n)$: $k \leftarrow \mathsf{Gen}(1^n)$, the adversary gets $1^n$ and oracle access to $\mathsf{Enc}_k$ (cpa), or to $\mathsf{Enc}_k$ and $\mathsf{Dec}_k$ (cca), a uniform bit $b$ selects the challenge, and the experiment outputs $1$ iff $b' = b$. Security is $\Pr[\mathsf{PrivK} = 1] \leq 1/2 + \mathsf{negl}(n)$. This bit-guessing form is half of the advantage above, since $2\Pr[b' = b] - 1 = \Pr[\mathsf{Expt}_1 = 1] - \Pr[\mathsf{Expt}_0 = 1]$. The adversary of `[KL]` is already one machine that keeps its oracles after the challenge.
> - `[BS]` writes the output bit $\hat b$ and the event $W_b$ that $\mathcal A$ outputs $1$ in Experiment $b$, so $\text{SSadv}[\mathcal A, \mathcal E] = |\Pr[W_0] - \Pr[W_1]|$. In its Attack Game 2.1 the challenger picks $k$ only after $\mathcal A$ has sent $m_0, m_1$; with no query, that changes nothing. Its bit-guessing versions $\text{SSadv}^*$, $\text{CPAadv}^*$, … are half of the difference forms: $\text{SSadv}[\mathcal A, \mathcal E] = 2 \cdot \text{SSadv}^*[\mathcal A, \mathcal E]$ `[BS Attack Game 2.4]`.

> [!remark]
> 1. ATK here is a placeholder for the attack. Unlike [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme (Old)#Indistinguishability\|PKE]], there is no public key, so even IND-CPA requires an explicit encryption oracle.
> 2. 1CCA security restricts the adversary to a single encryption query; it is the notion used in [[knowledge/cryptography/primitive/message authentication/Authenticated Encryption\|Authenticated Encryption]]. It is stated in the multi-challenge form below.

#### Multi-challenge form: CPA and CCA security

> [!definition] Parameters
> - $\mathcal E = (E, D)$: a cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$ — a SKE whose $\mathsf{KeyGen}$ samples $k \xleftarrow{\$} \mathcal K$, in the notation of `[BS]`.
> - $\mathsf{atk} \in \{\mathsf{cpa}, \mathsf{cca}\}$: the attack.
> - $Q_e$, $Q_d$: the maximal numbers of encryption and decryption queries.

> [!definition] CPA and CCA Security
> ### Scope
> A cipher $\mathcal E = (E, D)$ and all efficient adversaries.
>
> ---
> ### Condition
> - **Access** — every encryption query is a *pair* of messages, answered with an encryption of one of them, the same side in every query: there is no separate challenge.
>     - $\mathsf{cpa}$: encryption queries only — row 2.
>     - $\mathsf{cca}$: encryption and decryption queries, interleaved in any order — rows 2 and 3.
> - **Promise** — every encryption query has $|m_{i,0}| = |m_{i,1}|$; every decryption query has $\hat c_j \notin \{c_1, c_2, \dots\}$, the answers to the earlier encryption queries.
> - **Quantifier** — $\forall$ efficient $\mathcal A$; **1CCA** restricts to $Q_e = 1$.
> - **Adaptivity** — each query may depend on the earlier answers. Up to $Q_e$ challenges under one hidden branch.
>
> ---
> ### Experiment
> A distinguishing game: two branches that differ in the answer of row 2 only. `[BS Attack Game 5.2]` ($\mathsf{cpa}$), `[BS Attack Game 9.2]` ($\mathsf{cca}$).
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $k \xleftarrow{\$} \mathcal K$ | | |
> | 2 | | $\xleftarrow{\ m_{i,0},\, m_{i,1}\ }$ | **Encryption queries** (repeated, adaptive, at most $Q_e$ times): chooses $m_{i,0}, m_{i,1} \in \mathcal M$ with $\lvert m_{i,0} \rvert = \lvert m_{i,1} \rvert$ |
> | | **Game 0**: $c_i \leftarrow E(k, m_{i,0})$<br>**Game 1**: $c_i \leftarrow E(k, m_{i,1})$ | $\xrightarrow{\ c_i\ }$ | |
> | 3 | | $\xleftarrow{\ \hat c_j\ }$ | **Decryption queries** (repeated, adaptive, at most $Q_d$ times; $\mathsf{cca}$ only): sends $\hat c_j \in \mathcal C$ with $\hat c_j \notin \{c_1, c_2, \dots\}$ |
> | | $\hat m_j \leftarrow D(k, \hat c_j)$ | $\xrightarrow{\ \hat m_j\ }$ | |
> | 4 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}^{\mathsf{atk}}_b(\mathcal A)$, the bit $b'$ in Game $b$; the same branch answers every encryption query.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}^{\mathsf{atk}}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}^{\mathsf{atk}}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\text{CPAadv}[\mathcal A, \mathcal E] = \Big|\Pr\big[\mathsf{Expt}^{\mathsf{cpa}}_0(\mathcal A) = 1\big] - \Pr\big[\mathsf{Expt}^{\mathsf{cpa}}_1(\mathcal A) = 1\big]\Big|$$
> $$\text{CCAadv}[\mathcal A, \mathcal E] = \Big|\Pr\big[\mathsf{Expt}^{\mathsf{cca}}_0(\mathcal A) = 1\big] - \Pr\big[\mathsf{Expt}^{\mathsf{cca}}_1(\mathcal A) = 1\big]\Big|$$
> - $\mathcal E$ is **CPA secure** if $\text{CPAadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.
> - $\mathcal E$ is **CCA secure** if $\text{CCAadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$, and **1CCA secure** if this holds for every efficient $\mathcal A$ with $Q_e = 1$.
> - With $\mathsf{atk} = \mathsf{cpa}$ and $Q_e = 1$ this is `[BS Attack Game 2.1]` again: $\text{CPAadv}$ of a single-query adversary is $\text{SSadv}$.

> [!remark] The two forms
> The multi-challenge forms $\text{CPAadv}$ and $\text{CCAadv}$ are the versions used in the Construction theorems below and in [[knowledge/cryptography/primitive/message authentication/Authenticated Encryption\|Authenticated Encryption]]. `⚠️ CLAUDE – verify:` my reasoning, not taken from a source: an encryption query $m$ of the single-challenge game is the pair $(m, m)$ here and its challenge is one more pair, so a single-challenge advantage is at most the $\text{CPAadv}$ of a wrapper with one more query; conversely a hybrid over the $Q_e$ pairs gives $\text{CPAadv} \leq Q_e$ times a single-challenge advantage. The same argument applies to $\mathsf{cca}$.

#### Message recovery

> [!definition] Parameters
> - $\mathcal E = (E, D)$: a cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$, with $\mathcal M$ finite.

> [!definition] Message Recovery Security
> ### Scope
> A cipher $\mathcal E$ and all efficient adversaries.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ receives one encryption of a uniform message; no query.
> - **Promise** — none.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — none: one message from the challenger, one answer.
>
> ---
> ### Experiment
> A search game: one branch. `[BS Attack Game 2.2]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $m \xleftarrow{\$} \mathcal M$<br>$k \xleftarrow{\$} \mathcal K$<br>$c \leftarrow E(k, m)$ | $\xrightarrow{\ c\ }$ | |
> | 2 | | $\xleftarrow{\ \hat m\ }$ | outputs a message $\hat m \in \mathcal M$ |
> | 3 | compares $\hat m$ with $m$ | | |
>
> **Goal** — $\mathcal A$ wins iff:
> - $\hat m = m$.
>
> ---
> ### Property
> $$\text{MRadv}[\mathcal A, \mathcal E] = \Pr[\mathcal A \text{ wins}] - \frac{1}{|\mathcal M|}.$$
> - $\mathcal E$ is **message recovery secure** if $\text{MRadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.
> - $1/|\mathcal M|$ is the winning probability of a blind guess. `⚠️ CLAUDE – verify:` I believe `[BS]` takes the absolute value, $|\Pr[\mathcal A \text{ wins}] - 1/|\mathcal M||$; the formula above is the one this note had.

> [!theorem] Semantic Security $\Rightarrow$ Message Recovery Security
> If $\mathcal E$ is semantically secure, then $\text{MRadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

#### Parity prediction

> [!definition] Parameters
> - $\mathcal E = (E, D)$: a cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$ with $\mathcal M = \{0, 1\}^L$.
> - $\text{parity}(m)$: the XOR of the bits of $m$.

> [!definition] Parity Prediction Security
> ### Scope
> A cipher $\mathcal E$ and all efficient adversaries.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ receives one encryption of a uniform message; no query.
> - **Promise** — none.
> - **Quantifier** — $\forall$ efficient $\mathcal A$.
> - **Adaptivity** — none: one message from the challenger, one answer.
>
> ---
> ### Experiment
> A search game: one branch; the challenger acts as in the message recovery game. `[BS Attack Game 2.3]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $m \xleftarrow{\$} \mathcal M$<br>$k \xleftarrow{\$} \mathcal K$<br>$c \leftarrow E(k, m)$ | $\xrightarrow{\ c\ }$ | |
> | 2 | | $\xleftarrow{\ \hat b\ }$ | outputs a bit $\hat b \in \{0, 1\}$ |
> | 3 | computes $\text{parity}(m)$ | | |
>
> **Goal** — $\mathcal A$ wins iff:
> - $\hat b = \text{parity}(m)$.
>
> ---
> ### Property
> $$\text{Parityadv}[\mathcal A, \mathcal E] = \Big|\Pr[\mathcal A \text{ wins}] - \frac{1}{2}\Big|.$$
> - $\mathcal E$ is **parity prediction secure** if $\text{Parityadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

> [!theorem] Semantic Security $\Rightarrow$ Parity Prediction Security
> If $\mathcal E$ is semantically secure, then $\text{Parityadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

### Multi-key Semantic Security

> [!definition] Parameters
> - $\mathcal E = (E, D)$: a cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$ — a SKE whose $\mathsf{KeyGen}$ samples $k \xleftarrow{\$} \mathcal K$, in the notation of `[BS]`.
> - $Q$: the maximal number of queries. $t$: the running-time bound. $\varepsilon$: the advantage bound.

> [!definition] SKE Multi-key Semantic Security
> ### Scope
> A cipher $\mathcal E$ and all adversaries of running time at most $t$.
>
> ---
> ### Condition
> - **Access** — each query is a pair of messages, answered with an encryption of one of them under a **fresh key**; the same side in every query.
> - **Promise** — every query has $|m_{i,0}| = |m_{i,1}|$.
> - **Quantifier** — $\forall \mathcal A$ of running time at most $t$.
> - **Adaptivity** — each query may depend on the earlier answers.
>
> ---
> ### Experiment
> A distinguishing game: two branches that differ in the answer of row 1 only. `[BS Attack Game 5.1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | | $\xleftarrow{\ m_{i,0},\, m_{i,1}\ }$ | **Queries** (repeated, adaptive, at most $Q$ times): chooses $m_{i,0}, m_{i,1} \in \mathcal M$ with $\lvert m_{i,0} \rvert = \lvert m_{i,1} \rvert$ |
> | | $k_i \xleftarrow{\$} \mathcal K$<br>**Game 0**: $c_i \leftarrow E(k_i, m_{i,0})$<br>**Game 1**: $c_i \leftarrow E(k_i, m_{i,1})$ | $\xrightarrow{\ c_i\ }$ | |
> | 2 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}^{\mathsf{mss}}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}^{\mathsf{mss}}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}^{\mathsf{mss}}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\text{Adv}_\text{SKE}^{\text{mss}}(\mathcal A) = \text{MSSadv}[\mathcal A, \mathcal E] = \Big|\Pr\big[\mathsf{Expt}^{\mathsf{mss}}_0(\mathcal A) = 1\big] - \Pr\big[\mathsf{Expt}^{\mathsf{mss}}_1(\mathcal A) = 1\big]\Big|.$$
> - **$(t,\varepsilon)$-multi-key semantic security** — a SKE scheme is $(t, \varepsilon)$-multi-key semantically secure if $\text{Adv}_\text{SKE}^{\text{mss}}(\mathcal A) \leq \varepsilon$ for every adversary $\mathcal A$ with running time at most $t$.
> - $\mathcal E$ is **multi-key semantically secure** if $\text{MSSadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

> [!theorem]
> If $\mathcal E$ is semantically secure, it is multi-key semantically secure. For every MSS adversary $\mathcal A$ making at most $Q$ queries, there exists an SS adversary $\mathcal B$ ([[knowledge/cryptography/foundations/Elementary Wrapper\|elementary wrapper]]) such that $$\text{MSSadv}[\mathcal A, \mathcal E] = Q \cdot \text{SSadv}[\mathcal B, \mathcal E].$$

### Nonce-based CPA Security

> [!definition] Parameters
> - $\mathcal E = (E, D)$: a nonce-based cipher defined over $(\mathcal K, \mathcal M, \mathcal C, \mathcal N)$; $E(k, m, n)$ and $D(k, c, n)$ take a nonce $n \in \mathcal N$.
> - $Q$: the maximal number of queries. $t$: the running-time bound. $\varepsilon$: the advantage bound.

> [!definition] SKE nCPA Security
> ### Scope
> A nonce-based cipher $\mathcal E$ and all adversaries of running time at most $t$.
>
> ---
> ### Condition
> - **Access** — each query is a pair of messages and a nonce, answered with an encryption of one of the messages under that nonce; the same side in every query.
> - **Promise** — every query has $|m_{i,0}| = |m_{i,1}|$ and a new nonce, $n_i \notin \{n_1, \dots, n_{i-1}\}$.
> - **Quantifier** — $\forall \mathcal A$ of running time at most $t$.
> - **Adaptivity** — each query, nonce included, may depend on the earlier answers.
>
> ---
> ### Experiment
> A distinguishing game: two branches that differ in the answer of row 2 only. `[BS Attack Game 5.3]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $k \xleftarrow{\$} \mathcal K$ | | |
> | 2 | | $\xleftarrow{\ m_{i,0},\, m_{i,1},\, n_i\ }$ | **Queries** (repeated, adaptive, at most $Q$ times): chooses $m_{i,0}, m_{i,1} \in \mathcal M$ with $\lvert m_{i,0} \rvert = \lvert m_{i,1} \rvert$ and a nonce $n_i \in \mathcal N \setminus \{n_1, \dots, n_{i-1}\}$ |
> | | **Game 0**: $c_i \leftarrow E(k, m_{i,0}, n_i)$<br>**Game 1**: $c_i \leftarrow E(k, m_{i,1}, n_i)$ | $\xrightarrow{\ c_i\ }$ | |
> | 3 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}^{\mathsf{ncpa}}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}^{\mathsf{ncpa}}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}^{\mathsf{ncpa}}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\text{Adv}_\text{SKE}^{\text{ncpa}}(\mathcal A) = \text{nCPAadv}[\mathcal A, \mathcal E] = \Big|\Pr\big[\mathsf{Expt}^{\mathsf{ncpa}}_0(\mathcal A) = 1\big] - \Pr\big[\mathsf{Expt}^{\mathsf{ncpa}}_1(\mathcal A) = 1\big]\Big|.$$
> - **$(t,\varepsilon)$-nCPA security** — a nonce-based SKE scheme is $(t, \varepsilon)$-nCPA secure if $\text{Adv}_\text{SKE}^{\text{ncpa}}(\mathcal A) \leq \varepsilon$ for every adversary $\mathcal A$ with running time at most $t$.
> - $\mathcal E$ is **nCPA secure** if $\text{nCPAadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

> [!remark]
> Integrity notions — ciphertext integrity (CI) and AE security — live in [[knowledge/cryptography/primitive/message authentication/Authenticated Encryption\|Authenticated Encryption]]. The distribution-distinguishing toolkit ($\text{Distadv}$, statistical distance, data-processing inequality) lives in [[knowledge/cryptography/foundations/Indistinguishability\|Indistinguishability]] and [[knowledge/math/probability/Statistical Distance\|Statistical Distance]]. The guessing-advantage game lives in [[knowledge/cryptography/primitive/key establishment/Key Derivation Problem\|Key Derivation Problem]].

## Construction

### CPA-Secure Cipher Constructions

#### Generic Hybrid Construction

> [!construction] Generic Hybrid
> Let $\mathcal E = (E, D)$ be a cipher over $(\mathcal K, \mathcal M, \mathcal C)$. Let $F$ be a PRF over $(\mathcal K', \mathcal X, \mathcal K)$. Define a new cipher $\mathcal E' = (E', D')$ over $(\mathcal K', \mathcal M, \mathcal X \times \mathcal C)$:
> - $E'(k', m)$: $x \xleftarrow{R} \mathcal X, k \leftarrow F(k', x), c \xleftarrow{R} E(k, m)$; output $(x, c)$.
> - $D'(k', (x, c))$: $k \leftarrow F(k', x), m \leftarrow D(k, c)$; output $m$.

> [!theorem]
> If $F$ is a secure PRF, $\mathcal E$ is semantically secure, and $N = |\mathcal X|$ is super-poly, then $\mathcal E'$ is CPA secure. For every CPA adversary $\mathcal A$ making at most $Q$ queries, there exist PRF adversary $\mathcal B_F$ and SS adversary $\mathcal B_{\mathcal E}$ (elementary wrappers around $\mathcal A$) such that $$\text{CPAadv}[\mathcal A, \mathcal E'] \leq \frac{Q^2}{N} + 2 \cdot \text{PRFadv}[\mathcal B_F, F] + Q \cdot \text{SSadv}[\mathcal B_{\mathcal E}, \mathcal E].$$

#### Randomized Counter Mode

> [!construction] Randomized Counter Mode
> Suppose $F$ is a PRF defined over $(\mathcal K, \mathcal X, \mathcal Y)$ with $\mathcal X = \{0, \dots, N - 1\}$ and $\mathcal Y = \{0, 1\}^n$. For poly-bounded $\ell \geq 1$, define cipher $\mathcal E = (E, D)$ with key space $\mathcal K$, message space $\mathcal Y^{\leq \ell}$, and ciphertext space $\mathcal X \times \mathcal Y^{\leq \ell}$:
> $E(k, m)$ with $v = |m|$:
> 1. $x \xleftarrow{R} \mathcal X$
> 2. For $j \leftarrow 0$ to $v - 1$: $c[j] \leftarrow F(k, x + j \bmod N) \oplus m[j]$
> 3. Output $(x, c)$
>
> $D(k, (x, c))$ with $v = |c|$:
> 1. For $j \leftarrow 0$ to $v - 1$: $m[j] \leftarrow F(k, x + j \bmod N) \oplus c[j]$
> 2. Output $m$

> [!remark]
> The $x$ component is typically called an **initial value** or **IV**.

> [!theorem]
> If $F$ is a secure PRF and $N$ is super-poly, then $\mathcal E$ is CPA secure. For every CPA adversary $\mathcal A$ making at most $Q$ queries, there exists a PRF adversary $\mathcal B$ (elementary wrapper) such that $$\text{CPAadv}[\mathcal A, \mathcal E] \leq \frac{2Q^2 \ell}{N} + 2 \cdot \text{PRFadv}[\mathcal B, F].$$

#### Cipher Block Chaining Mode

> [!construction] CBC Mode
> Let $\mathcal E = (E, D)$ be a block cipher over $(\mathcal K, \mathcal X)$ with $\mathcal X = \{0, 1\}^n$ and $N = |\mathcal X| = 2^n$. For poly-bounded $\ell \geq 1$, define $\mathcal E' = (E', D')$ with key space $\mathcal K$, message space $\mathcal X^{\leq \ell}$, and ciphertext space $\mathcal X^{\ell + 1} \setminus \mathcal X^0$:
> $E'(k, m)$ with $v = |m|$:
> 1. $c[0] \xleftarrow{R} \mathcal X$
> 2. For $j \leftarrow 0$ to $v - 1$: $c[j + 1] \leftarrow E(k, c[j] \oplus m[j])$
> 3. Output $c$
>
> $D'(k, c)$ with $v = |c| - 1$:
> 1. For $j \leftarrow 0$ to $v - 1$: $m[j] \leftarrow D(k, c[j + 1]) \oplus c[j]$
> 2. Output $m$

> [!theorem]
> If $\mathcal E$ is a secure block cipher and $N$ is super-poly, then $\mathcal E'$ is CPA secure. For every CPA adversary $\mathcal A$ making at most $Q$ queries, there exists a block-cipher adversary $\mathcal B$ (elementary wrapper) such that $$\text{CPAadv}[\mathcal A, \mathcal E'] \leq \frac{2Q^2 \ell^2}{N} + 2 \cdot \text{BCadv}[\mathcal B, \mathcal E].$$

### Nonce-Based CPA Constructions

#### Nonce-based Generic Hybrid

> [!construction] Nonce-based Generic Hybrid
> Let $\mathcal E = (E, D)$ be a cipher over $(\mathcal K, \mathcal M, \mathcal C)$ and $F$ a PRF over $(\mathcal K', \mathcal X, \mathcal K)$. Define the nonce-based cipher $\mathcal E'$ over $(\mathcal K', \mathcal M, \mathcal C, \mathcal X)$:
> - $E'(k', m, x) = E(k, m)$ where $k = F(k', x)$.
> - $D'(k', c, x) = D(k, c)$ where $k = F(k', x)$.

> [!theorem]
> If $F$ is a secure PRF and $\mathcal E$ is semantically secure, then $\mathcal E'$ is nCPA secure. For every nCPA adversary $\mathcal A$ making at most $Q$ queries, there exist PRF adversary $\mathcal B_F$ and SS adversary $\mathcal B_{\mathcal E}$ (elementary wrappers) such that $$\text{nCPAadv}[\mathcal A, \mathcal E'] \leq 2 \cdot \text{PRFadv}[\mathcal B_F, F] + Q \cdot \text{SSadv}[\mathcal B_{\mathcal E}, \mathcal E].$$

#### Nonce-based Counter Mode

> [!construction] Nonce-based Counter Mode
> Assume $\ell$ divides $N$. Modify the [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Randomized Counter Mode\|#Randomized Counter Mode]] scheme by using nonce space $\{0, \dots, N/\ell - 1\}$ and translating the nonce $n$ to PRF input $x = n\ell$.

> [!theorem]
> If $F$ is a secure PRF, $\mathcal E$ is nCPA secure. For every nCPA adversary $\mathcal A$, there exists a PRF adversary $\mathcal B$ (elementary wrapper) such that $$\text{nCPAadv}[\mathcal A, \mathcal E] \leq 2 \cdot \text{PRFadv}[\mathcal B, F].$$

#### Nonce-based CBC Mode

> [!construction] Nonce-based CBC Mode
> Assume PRF $F$ over $(\mathcal K', \mathcal N, \mathcal X)$, where $\mathcal X$ matches the block space of underlying block cipher $\mathcal E = (E, D)$ over $(\mathcal K, \mathcal X)$. In the nonce-based CBC scheme $\mathcal E'$, key space is $\mathcal K \times \mathcal K'$, and the IV is computed from the nonce $n$ and the key $k'$ as $c[0] = F(k', n)$.

> [!theorem]
> If $\mathcal E$ is a secure block cipher, $N$ is super-poly, and $F$ is a secure PRF, then for any poly-bounded $\ell \geq 1$, $\mathcal E'$ is nCPA secure. For every nCPA adversary $\mathcal A$ making at most $Q$ queries, there exist block-cipher adversary $\mathcal B$ and PRF adversary $\mathcal B_F$ (elementary wrappers) such that $$\text{nCPAadv}[\mathcal A, \mathcal E'] \leq \frac{2Q^2 \ell^2}{N} + 2 \cdot \text{PRFadv}[\mathcal B_F, F] + 2 \cdot \text{BCadv}[\mathcal B, \mathcal E].$$

## Case Study

### One-time Pad — Canonical Perfectly-Secure Cipher

See [[knowledge/cryptography/primitive/symmetric encryption/classical/One-time Pad\|One-time Pad]]. The one-time pad is the canonical example of [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Perfect Security\|perfect security]]: $\mathcal K = \mathcal M = \mathcal C = \{0, 1\}^L$ with $E(k, m) = D(k, m) = k \oplus m$. By Shannon's Theorem this achieves the minimum-possible $|\mathcal K| = |\mathcal M|$ for any perfectly-secure cipher.

### Classical schemes

See  for the historical schemes: [[knowledge/cryptography/primitive/symmetric encryption/classical/Substitution Cipher\|Substitution Cipher]], [[knowledge/cryptography/primitive/symmetric encryption/classical/Multiplicative Encryption\|Multiplicative Encryption]], [[knowledge/cryptography/primitive/symmetric encryption/classical/Affine Cipher\|Affine Cipher]], [[knowledge/cryptography/primitive/symmetric encryption/classical/Hill Cipher\|Hill Cipher]], [[knowledge/cryptography/primitive/symmetric encryption/classical/Vigenère cipher\|Vigenère cipher]], and others. These illustrate the development of the field but are insecure by modern standards.

### Modern schemes

See  for deployed modern ciphers (AES, ChaCha20, DES, …).
