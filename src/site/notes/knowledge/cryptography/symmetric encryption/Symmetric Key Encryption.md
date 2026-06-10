---
{"dg-publish":true,"permalink":"/knowledge/cryptography/symmetric-encryption/symmetric-key-encryption/","dg-note-properties":{}}
---


| Term                                                      | Reference                                   |                    |
| --------------------------------------------------------- | ------------------------------------------- | ------------------ |
| Attack Game 2.1 (Semantic Security)                       | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Semantic Security\|#Semantic Security]]                      | $\text{SSadv}$     |
| Attack Game 2.2 (Message Recovery)                        | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Message Recovery\|#Message Recovery]]                       | $\text{MRadv}$     |
| Attack Game 2.3 (Parity Prediction)                       | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Parity Prediction\|#Parity Prediction]]                      | $\text{Parityadv}$ |
| Attack Game 2.4 (Semantic Security: Bit-guessing Version) | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Semantic Security Bit-guessing Version\|#Semantic Security Bit-guessing Version]] | $\text{SSadv}^*$   |
| Attack Game 3.3 (Distinguishing $P_0$ from $P_1$)         | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Indistinguishability\|#Indistinguishability]]                   | $\text{Distadv}$   |
| Attack Game 5.1 (Multi-key Semantic Security)             | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Multi-key Semantic Security\|#Multi-key Semantic Security]]            | $\text{MSSadv}$    |
| Attack Game 5.2 (CPA Security)                            | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Chosen Plaintext Attack Security\|#Chosen Plaintext Attack Security]]       | $\text{CPAadv}$    |
| Attack Game 5.3 (Nonce-based CPA Security)                | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Nonce-based CPA Security\|#Nonce-based CPA Security]]               | $\text{nCPAadv}$   |
| Attack Game 8.3 (Guessing Advantage)                      | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Key Derivation Problem\|#Key Derivation Problem]]                 | $\text{Guessadv}$  |
| Attack Game 9.1 (Ciphertext Integrity)                    | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Ciphertext Integrity\|#Ciphertext Integrity]]                   | $\text{CIadv}$     |
| Attack Game 9.2 (Chosen Ciphertext Attack)                | [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Chosen Ciphertext Attack Security\|#Chosen Ciphertext Attack Security]]      | $\text{CCAadv}$    |

## Syntax

> [!definition] Symmetric Key Encryption Scheme
> A **symmetric key encryption scheme** $\text{SKE} = (\text{Enc}, \text{Dec})$ is a pair of efficient algorithms with a message space $\mathcal M$, ciphertext space $\mathcal C$ and a key space $\mathcal K$.
> - $k \leftarrow \text{KeyGen}$: The key generation randomized algorithm that outputs a key $k \in \mathcal K$. 
> - $c \leftarrow \text{Enc}(k, m)$: The encryption algorithm takes a key $k \in \mathcal K$ and a message $m$ to produce a ciphertext $c$.
> - $m \leftarrow \text{Dec}(k, c)$: The decryption algorithm takes a key $k \in \mathcal K$ and a ciphertext $c$ to produce a message $m$.

> [!algorithm] Computational Cipher (Mathematical Detail)
> Let $\mathcal E = (E, D)$ be a computational cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. We associate with $\mathcal E$ families of key, message, and ciphertext spaces, indexed by
> - A **security parameter** $\lambda \in \mathbb Z_{\geq 1}$, and
> - A **system parameter** $\Lambda$ (a bit string).
>
> Thus, instead of finite sets, we have families $\{\mathcal K_{\lambda, \Lambda}\}, \{\mathcal M_{\lambda, \Lambda}\}, \{\mathcal C_{\lambda, \Lambda}\}$ such that:
> 1. $K, M, C$ are efficiently recognizable.
> 2. $K$ is efficiently sampleable.
> 3. $M$ has an effective length function.
> 4. $E$ is an efficient probabilistic algorithm that on input $\lambda, \Lambda, k, m$ outputs an element of $\mathcal C_{\lambda, \Lambda}$.
> 5. $D$ is an efficient deterministic algorithm that on input $\lambda, \Lambda, k, c$ outputs either an element of $\mathcal M_{\lambda, \Lambda}$ or the special symbol $\text{reject} \notin \mathcal M_{\lambda, \Lambda}$.
> 6. Correctness: for all valid inputs, $D(\lambda, \Lambda; k, E(\lambda, \Lambda; k, m)) = m$.

## Property

### Correctness

> [!definition] Correctness
> A symmetric cipher $\mathcal E = (E, D)$ is **correct** if for all keys $k \in \mathcal K$ and all messages $m \in \mathcal M$: $$D(k, E(k, m)) = m.$$

### Uniformity

> [!definition] $\gamma$-Uniformity
> For given $k \in \mathcal K, m \in \mathcal M$ and $c \in \mathcal C$, define $$\gamma(m, c) = \Pr[c = E(k, m; r) \;|\; r \in \mathcal R].$$
> We say that a symmetric cipher $\mathcal E$ is $\gamma$-uniform if: $$\forall k \in \mathcal K, m \in \mathcal M, c \in \mathcal C: \gamma(m, c) \leq \gamma.$$
> Equivalently, in *bit* form ($\gamma$-spreadness, Hofheinz-Hövelmanns-Kiltz 2017): the ciphertext distribution has min-entropy at least $\gamma$ bits for every fixed message and key.

## Security

### Perfect Security

> [!definition] Perfect Security
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. Consider a probabilistic experiment in which the random variable $K$ is uniformly distributed over $\mathcal K$. If for all $m_0, m_1 \in \mathcal M$ and all $c \in \mathcal C$: $$P[E(K, m_0) = c] = P[E(K, m_1) = c],$$ then $\mathcal E$ is **perfectly secure**.

> [!theorem] Equivalent Characterizations of Perfect Security
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. The following are equivalent:
> 1. $\mathcal E$ is perfectly secure.
> 2. For every $c \in \mathcal C$, there exists an integer $N_c$ (possibly depending on $c$) such that for all $m \in \mathcal M$: $$|\{k \in \mathcal K : E(k, m) = c\}| = N_c.$$
> 3. If $K$ is uniformly distributed over $\mathcal K$, then each of the random variables $E(K, m)$, for $m \in \mathcal M$, has the same distribution.

> [!theorem] Predicate Form
> Consider a probabilistic experiment in which $K$ is uniformly distributed over $\mathcal K$. Then $\mathcal E$ is perfectly secure iff for every predicate $\phi$ on $\mathcal C$, and for all $m_0, m_1 \in \mathcal M$: $$P[\phi(E(K, m_0))] = P[\phi(E(K, m_1))].$$

> [!theorem] Independence Form
> Consider a random experiment in which $K$ and $M$ are random variables such that $K$ is uniform over $\mathcal K$, $M$ is distributed over $\mathcal M$, and $K \perp M$. Let $C = E(K, M)$. Then:
> - If $\mathcal E$ is perfectly secure, then $C$ and $M$ are independent.
> - Conversely, if $C$ and $M$ are independent and each message in $\mathcal M$ occurs with nonzero probability, then $\mathcal E$ is perfectly secure.

> [!theorem] Shannon's Theorem
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. If $\mathcal E$ is perfectly secure, then $|\mathcal K| \geq |\mathcal M|$.

> [!theorem] Generalized Shannon's Theorem
> Let $\mathcal E$ be a cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. Suppose [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Semantic Security\|semantic security]] advantage $\text{SSadv}[\mathcal A, \mathcal E] \leq \epsilon$ for all adversaries $\mathcal A$, including **computationally unbounded** ones. Then $|\mathcal K| \geq (1 - \epsilon) |\mathcal M|$.

### Indistinguishability under the Eavesdropping Attacks

> [!definition] IND-EAV Advantage
> For any adversary $\mathcal A = (\mathcal A_\text{find}, \mathcal A_\text{guess})$, we define the IND-EAV advantage: 
> $$\text{Adv}_{\text{SKE}}^{\text{EAV}} = 
> \left|\; \Pr\!\left[ b = b' \;\middle | \; 
> \begin{array}{l}
> (pk, sk) \leftarrow \text{KeyGen}(); \\
> (m_0, m_1, s) \leftarrow \mathcal A_\text{find}(pk); \\
> b \leftarrow \{0, 1\}; c^* \leftarrow \text{Enc}(pk, m_b); \\
> b' \leftarrow \mathcal A_\text{guess}(s, c^*)
> \end{array} \right] 
> \;- \frac{1}{2}
> \right|.$$

> [!definition] $(t, \varepsilon)$-IND-EAV security of a SKE
> A SKE scheme is $(t, \varepsilon)$**-IND-EAV secure** if for every adversary $\mathcal A$ that has running time bounded by $t$, we have $$\text{Adv}_\text{SKE}^{\text{EAV}} \leq \varepsilon$$

#### Message Recovery

> [!algorithm] Message Recovery
> For a given cipher $\mathcal E = (E, D)$, the attack game proceeds as follows:
> - The challenger computes $m \xleftarrow{R} \mathcal M, k \xleftarrow{R} \mathcal K, c \xleftarrow{R} E(k, m)$, and sends $c$ to the adversary.
> - The adversary outputs a message $\hat{m} \in \mathcal M$.
>
> Let $W$ be the event that $\hat{m} = m$. Define $$\text{MRadv}[\mathcal A, \mathcal E] = \Pr[W] - 1/|\mathcal M|.$$

> [!definition] Security Against Message Recovery
> A cipher $\mathcal E$ is **secure against message recovery** if for all efficient adversaries $\mathcal A$, $\text{MRadv}[\mathcal A, \mathcal E]$ is negligible.

> [!theorem]
> If $\mathcal E$ is semantically secure then $\mathcal E$ is secure against message recovery.

#### Parity Prediction

> [!algorithm] Parity Prediction
> For a given cipher $\mathcal E = (E, D)$, the attack game proceeds as follows:
> - The challenger computes $m \xleftarrow{R} \mathcal M, k \xleftarrow{R} \mathcal K, c \xleftarrow{R} E(k, m)$, and sends $c$ to the adversary.
> - The adversary outputs $\hat{b} \in \{0, 1\}$.
>
> Let $W$ be the event that $\hat{b} = \text{parity}(m)$. Define $$\text{Parityadv}[\mathcal A, \mathcal E] = |P[W] - 1/2|.$$

> [!definition] Parity Prediction Security
> A cipher $\mathcal E$ is **secure against parity prediction** if for all efficient adversaries $\mathcal A$, $\text{Parityadv}[\mathcal A, \mathcal E]$ is negligible.

> [!theorem]
> Let $\mathcal E$ be a cipher with $\mathcal M = \{0, 1\}^L$. If $\mathcal E$ is semantically secure, then $\mathcal E$ is secure against parity prediction.

#### Semantic Security: Bit-guessing Version

> [!algorithm] Semantic Security: Bit-guessing Version
> The attack game runs as follows:
> - The adversary computes $m_0, m_1 \in \mathcal M$, of the same length, and sends them to the challenger.
> - The challenger computes $b \xleftarrow{R} \{0, 1\}, k \xleftarrow{R} \mathcal K, c \xleftarrow{R} E(k, m_b)$, and sends $c$ to the adversary.
> - The adversary outputs $\hat{b} \in \{0, 1\}$.
>
> $\mathcal A$ **wins** if $\hat{b} = b$.

> [!definition] Bit-guessing Semantic Security
> If $W$ denotes the event that $\mathcal A$ wins, define $$\text{SSadv}^*[\mathcal A, \mathcal E] = |P[W] - 1/2|.$$

> [!theorem]
> For every cipher $\mathcal E$ and every adversary $\mathcal A$: $$\text{SSadv}[\mathcal A, \mathcal E] = 2 \cdot \text{SSadv}^*[\mathcal A, \mathcal E].$$

### Indistinguishability

> [!algorithm] Distinguishing $P_0$ from $P_1$
> For probability distributions $P_0$ and $P_1$ on a finite set $\mathcal R$, and adversary $\mathcal A$, define two experiments. For $b = 0, 1$:
> **Experiment $b$:**
> - The challenger samples $x \xleftarrow{R} P_b$ and sends $x$ to the adversary.
> - The adversary outputs $\hat{b} \in \{0, 1\}$.
>
> Let $W_b$ be the event that $\mathcal A$ outputs 1 in Experiment $b$. Define $$\text{Distadv}[\mathcal A, P_0, P_1] = |P[W_0] - P[W_1]|.$$

> [!definition] Computational Indistinguishability
> $P_0$ and $P_1$ are **computationally indistinguishable** if $\text{Distadv}[\mathcal A, P_0, P_1]$ is negligible for all efficient adversaries.

> [!definition] Statistical Distance
> $$\Delta[P_0, P_1] = \frac{1}{2} \sum_{r \in \mathcal R} |P_0(r) - P_1(r)|.$$

> [!theorem]
> $$\max_{\mathcal R' \subseteq \mathcal R}|P_0[\mathcal R'] - P_1[\mathcal R']| = \Delta[P_0, P_1].$$

> [!theorem]
> For every adversary $\mathcal A$: $\text{Distadv}[\mathcal A, P_0, P_1] \leq \Delta[P_0, P_1]$.

> [!definition] Statistical Indistinguishability
> $P_0$ and $P_1$ are **statistically indistinguishable** if $\Delta[P_0, P_1]$ is negligible.

> [!corollary]
> Statistical indistinguishability implies computational indistinguishability.

> [!theorem] Data-Processing Inequality
> If $f: \mathcal S \rightarrow \mathcal T$ is a function and $X, Y$ are random variables on $\mathcal S$, then $\Delta[f(X), f(Y)] \leq \Delta[X, Y]$.

### Multi-key Semantic Security

> [!algorithm] Multi-key Semantic Security
> For $b = 0, 1$, **Experiment $b$:**
> - The adversary submits a sequence of queries. For $i = 1, 2, \dots$, the $i$-th query is $(m_{i0}, m_{i1}) \in \mathcal M^2$, of the same length. The challenger computes $k_i \xleftarrow{R} \mathcal K, c_i \xleftarrow{R} E(k_i, m_{ib})$, and sends $c_i$ to the adversary.
> - The adversary outputs $\hat{b} \in \{0, 1\}$.
>
> Define $\text{MSSadv}[\mathcal A, \mathcal E] = |P[W_0] - P[W_1]|.$

> [!definition] Multi-key Semantic Security
> A cipher $\mathcal E$ is **multi-key semantically secure** if $\text{MSSadv}[\mathcal A, \mathcal E]$ is negligible for all efficient $\mathcal A$.

> [!theorem]
> If $\mathcal E$ is semantically secure, it is multi-key semantically secure. For every MSS adversary $\mathcal A$ making at most $Q$ queries, there exists an SS adversary $\mathcal B$ (elementary wrapper) such that $$\text{MSSadv}[\mathcal A, \mathcal E] = Q \cdot \text{SSadv}[\mathcal B, \mathcal E].$$

### Chosen Plaintext Attack Security

> [!algorithm] CPA Security
> For $b = 0, 1$, **Experiment $b$:**
> - The challenger selects $k \xleftarrow{R} \mathcal K$.
> - The adversary submits queries $(m_{i0}, m_{i1})$ for $i = 1, 2, \dots$ The challenger computes $c_i \xleftarrow{R} E(k, m_{ib})$ and returns $c_i$.
> - The adversary outputs $\hat{b} \in \{0, 1\}$.
>
> Define $\text{CPAadv}[\mathcal A, \mathcal E] = |P[W_0] - P[W_1]|.$

> [!definition] CPA Security
> A cipher $\mathcal E$ is called **CPA secure** if $\text{CPAadv}[\mathcal A, \mathcal E]$ is negligible for all efficient $\mathcal A$.

> [!definition] $(t, \varepsilon)$-CPA Security
> A cipher $\mathcal E$ is **$(t, \varepsilon)$-CPA secure** if every $\mathcal A$ running in time at most $t$ satisfies $\text{CPAadv}[\mathcal A, \mathcal E] \leq \varepsilon$.

> [!remark] Bit-guessing Version
> If the challenger chooses $b \in \{0, 1\}$ at random and runs Experiment $b$, define $\text{CPAadv}^*[\mathcal A, \mathcal E] = |P[\hat{b} = b] - 1/2|$. Then $\text{CPAadv}[\mathcal A, \mathcal E] = 2 \cdot \text{CPAadv}^*[\mathcal A, \mathcal E]$.

### Nonce-based CPA Security

> [!algorithm] Nonce-based CPA Security
> For a cipher $\mathcal E$ defined over $(\mathcal K, \mathcal M, \mathcal C, \mathcal N)$, for $b = 0, 1$:
> - The challenger selects $k \xleftarrow{R} \mathcal K$.
> - The adversary submits queries $(m_{i0}, m_{i1}, n_i)$ where $n_i \in \mathcal N \setminus \{n_1, \dots, n_{i-1}\}$. The challenger computes $c_i \leftarrow E(k, m_{ib}, n_i)$ and returns $c_i$.
> - The adversary outputs $\hat{b}$.
>
> Define $\text{nCPAadv}[\mathcal A, \mathcal E] = |P[W_0] - P[W_1]|.$

> [!definition] Nonce-based CPA Security
> A nonce-based cipher $\mathcal E$ is **nCPA secure** if $\text{nCPAadv}[\mathcal A, \mathcal E]$ is negligible for all efficient $\mathcal A$.

### Key Derivation Problem

> [!algorithm] Guessing Advantage
> Let $P$ be a probability distribution on a finite set $\mathcal S$ and let $I$ be a function on $\mathcal S$. For an adversary $\mathcal A$:
> - The challenger samples $s$ from $P$ and sends $I(s)$ to $\mathcal A$.
> - The adversary outputs $\hat{s}$ and wins if $\hat{s} = s$.
>
> Denote the winning probability by $\text{Guessadv}[\mathcal A, P, I]$.

### Ciphertext Integrity

> [!algorithm] Ciphertext Integrity
> For an adversary $\mathcal A$:
> - The challenger chooses $k \xleftarrow{R} \mathcal K$.
> - For $i = 1, 2, \dots$, $\mathcal A$ submits $m_i \in \mathcal M$; the challenger returns $c_i \xleftarrow{R} E(k, m_i)$.
> - $\mathcal A$ eventually outputs a candidate ciphertext $c \notin \{c_1, c_2, \dots\}$.
>
> $\mathcal A$ wins if $D(k, c) \neq \text{reject}$. Define $\text{CIadv}[\mathcal A, \mathcal E] = \Pr[\mathcal A \text{ wins}]$. $\mathcal A$ is a **$Q$-query adversary** if it issues at most $Q$ encryption queries.

> [!definition] Ciphertext Integrity
> A cipher $\mathcal E$ provides **ciphertext integrity** (CI) if $\text{CIadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

> [!definition] One-time Ciphertext Integrity
> $\mathcal E$ provides **one-time ciphertext integrity** if $\text{CIadv}[\mathcal A, \mathcal E]$ is negligible for every efficient single-query $\mathcal A$.

### Chosen Ciphertext Attack Security

> [!algorithm] CCA Security
> For $b = 0, 1$, **Experiment $b$:**
> - The challenger selects $k \xleftarrow{R} \mathcal K$.
> - $\mathcal A$ makes a series of queries of two types:
>   - **Encryption query**: $(m_{i0}, m_{i1}) \in \mathcal M^2$. The challenger returns $c_i \xleftarrow{R} E(k, m_{ib})$.
>   - **Decryption query**: $\hat{c_j} \in \mathcal C$ with $\hat{c_j} \notin \{c_1, c_2, \dots\}$. The challenger returns $\hat{m_j} \leftarrow D(k, \hat{c_j})$.
> - $\mathcal A$ outputs $\hat{b} \in \{0, 1\}$.
>
> Define $\text{CCAadv}[\mathcal A, \mathcal E] = |P[W_0] - P[W_1]|.$

> [!definition] CCA Security
> A cipher $\mathcal E$ is **CCA-secure** if $\text{CCAadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

> [!definition] 1CCA Security
> If $\mathcal A$ is restricted to a single encryption query, denote its advantage $\text{1CCAadv}$. $\mathcal E$ is **1CCA-secure** if $\text{1CCAadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

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
> Assume $\ell$ divides $N$. Modify the [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Randomized Counter Mode\|#Randomized Counter Mode]] scheme by using nonce space $\{0, \dots, N/\ell - 1\}$ and translating the nonce $n$ to PRF input $x = n\ell$.

> [!theorem]
> If $F$ is a secure PRF, $\mathcal E$ is nCPA secure. For every nCPA adversary $\mathcal A$, there exists a PRF adversary $\mathcal B$ (elementary wrapper) such that $$\text{nCPAadv}[\mathcal A, \mathcal E] \leq 2 \cdot \text{PRFadv}[\mathcal B, F].$$

#### Nonce-based CBC Mode

> [!construction] Nonce-based CBC Mode
> Assume PRF $F$ over $(\mathcal K', \mathcal N, \mathcal X)$, where $\mathcal X$ matches the block space of underlying block cipher $\mathcal E = (E, D)$ over $(\mathcal K, \mathcal X)$. In the nonce-based CBC scheme $\mathcal E'$, key space is $\mathcal K \times \mathcal K'$, and the IV is computed from the nonce $n$ and the key $k'$ as $c[0] = F(k', n)$.

> [!theorem]
> If $\mathcal E$ is a secure block cipher, $N$ is super-poly, and $F$ is a secure PRF, then for any poly-bounded $\ell \geq 1$, $\mathcal E'$ is nCPA secure. For every nCPA adversary $\mathcal A$ making at most $Q$ queries, there exist block-cipher adversary $\mathcal B$ and PRF adversary $\mathcal B_F$ (elementary wrappers) such that $$\text{nCPAadv}[\mathcal A, \mathcal E'] \leq \frac{2Q^2 \ell^2}{N} + 2 \cdot \text{PRFadv}[\mathcal B_F, F] + 2 \cdot \text{BCadv}[\mathcal B, \mathcal E].$$

## Case Study

### One-time Pad — Canonical Perfectly-Secure Cipher

See [[knowledge/cryptography/symmetric encryption/classical/One-time Pad\|One-time Pad]]. The one-time pad is the canonical example of perfect security: $\mathcal K = \mathcal M = \mathcal C = \{0, 1\}^L$ with $E(k, m) = D(k, m) = k \oplus m$. By Shannon's Theorem this achieves the minimum-possible $|\mathcal K| = |\mathcal M|$ for any perfectly-secure cipher.

### Classical schemes

See [[symmetric encryption/classical/\|classical/]] for the historical schemes: [[knowledge/cryptography/symmetric encryption/classical/Substitution Cipher\|Substitution Cipher]], [[knowledge/cryptography/symmetric encryption/classical/Multiplicative Encryption\|Multiplicative Encryption]], [[knowledge/cryptography/symmetric encryption/classical/Affine Cipher\|Affine Cipher]], [[knowledge/cryptography/symmetric encryption/classical/Hill Cipher\|Hill Cipher]], [[knowledge/cryptography/symmetric encryption/classical/Vigenère cipher\|Vigenère cipher]], and others. These illustrate the development of the field but are insecure by modern standards.

### Modern schemes

See [[symmetric encryption/schemes/\|schemes/]] for deployed modern ciphers (AES, ChaCha20, DES, …).
