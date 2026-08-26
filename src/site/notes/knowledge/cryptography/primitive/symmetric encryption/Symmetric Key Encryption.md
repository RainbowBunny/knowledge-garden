---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/symmetric-key-encryption/","dg-note-properties":{}}
---

## Syntax

> [!definition] Symmetric Key Encryption Scheme
> A **symmetric-key encryption scheme** $\text{SKE} = (\text{Gen}, \text{Enc}, \text{Dec})$ is a triple of efficient algorithms with a message space $\mathcal M$, ciphertext space $\mathcal C$, randomness space $\mathcal R$ and key space $\mathcal K$.
> - $k \leftarrow \text{Gen}()$: The key-generation algorithm $\text{Gen}$ returns a key $k \in \mathcal K$ (often simply $k \xleftarrow{\$} \mathcal K$).
> - $c \leftarrow \text{Enc}(k, m)$ (Deterministic) or $c \leftarrow \text{Enc}(k, m; r)$ (Probabilistic): The encryption algorithm takes a key $k \in \mathcal K$, a message $m \in \mathcal M$ and possibly an internal random $r \leftarrow \mathcal R$ to produce a ciphertext $c \in \mathcal C$.
> - $m \leftarrow \text{Dec}(k, c)$: The deterministic decryption algorithm takes a key $k \in \mathcal K$ and a ciphertext $c$, and outputs either a message $m \in \mathcal M$ or a special symbol $\perp$ to indicate **rejection**.

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

### Min-Entropy

> [!definition] Min-Entropy
> Given $k \in \mathcal K, m \in \mathcal M$, we define the **min-entropy** of $\text{Enc}(k, m)$ by
> $$\gamma(k, m) = -\log \max_{c \in \mathcal C} \Pr[c = \text{Enc}(k, m; r) \; | \; r \leftarrow \mathcal R].$$
> We say that a $\text{SKE}$ is $\gamma$**-spread** if:
> $$\forall k \in \mathcal K, m \in \mathcal M: \gamma(k, m) \geq \gamma$$

> [!remark]
> Equivalent formulation ($\gamma$-uniformity): $\mathcal E$ is $\gamma$-uniform if $\Pr[c = E(k, m; r) \;|\; r \in \mathcal R] \leq \gamma$ for all $k, m, c$. A $\gamma$-spread scheme is $2^{-\gamma}$-uniform (Hofheinz–Hövelmanns–Kiltz 2017). This matches the [[knowledge/cryptography/primitive/public-key encryption/Public Key Encryption#Min-Entropy\|PKE min-entropy]] definition.

## Security

### Perfect Security

> [!definition] Perfect Security
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. Consider a probabilistic experiment in which the random variable $K$ is uniformly distributed over $\mathcal K$. If for all $m_0, m_1 \in \mathcal M$ and all $c \in \mathcal C$: $$P[E(K, m_0) = c] = P[E(K, m_1) = c],$$ then $\mathcal E$ is **perfectly secure**.

> [!theorem] Shannon's Theorem
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. If $\mathcal E$ is perfectly secure, then $|\mathcal K| \geq |\mathcal M|$.

> [!theorem] Generalized Shannon's Theorem
> Let $\mathcal E$ be a cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. Suppose the semantic security advantage $\text{SSadv}[\mathcal A, \mathcal E] \leq \epsilon$ for all adversaries $\mathcal A$, including **computationally unbounded** ones. Then $|\mathcal K| \geq (1 - \epsilon) |\mathcal M|$.

> [!remark]
> The equivalent characterizations (counting form, predicate form, independence form) are collected in [[knowledge/cryptography/primitive/symmetric encryption/Perfect Security\|Perfect Security]]. The canonical perfectly secure cipher is the [[knowledge/cryptography/primitive/symmetric encryption/classical/One-time Pad\|One-time Pad]].

### Indistinguishability

> [!definition] SKE Indistinguishability Advantage
> For any adversary $\mathcal A = (\mathcal A_\text{find}, \mathcal A_\text{guess})$, we define the indistinguishability advantage:
> $$\text{Adv}_\text{SKE}^{\text{ind-atk}}(\mathcal A) =
> \left|\; \Pr\!\left[ b = b' \;\middle |\;
> \begin{array}{l}
> k \leftarrow \text{Gen}(); \\
> (m_0, m_1, s) \leftarrow \mathcal A_\text{find}^{\mathcal O_\text{find}}(); \\
> b \xleftarrow{\$} \{0, 1\}; c^* \leftarrow \text{Enc}(k, m_b); \\
> b' \leftarrow \mathcal A_\text{guess}^{\mathcal O_\text{guess}}(s, c^*)
> \end{array} \right]
> \;- \frac{1}{2}
> \right|.$$
> Where:
> 1. Eavesdropping Attack: $\text{atk} = \text{eav}$ then $\mathcal O_\text{find}(\cdot) = \varepsilon$ and $\mathcal O_\text{guess}(\cdot) = \varepsilon$.
> 2. Chosen Plaintext Attack: $\text{atk} = \text{cpa}$ then $\mathcal O_\text{find}(\cdot) = \text{Enc}(k, \cdot)$ and $\mathcal O_\text{guess}(\cdot) = \text{Enc}(k, \cdot)$.
> 3. Chosen Ciphertext Attack: $\text{atk} = \text{cca}$ then $\mathcal O_\text{find}(\cdot) = \{\text{Enc}(k, \cdot), \text{Dec}(k, \cdot)\}$ and $\mathcal O_\text{guess}(\cdot) = \{\text{Enc}(k, \cdot), \text{Dec}(k, \cdot)\}$.
>
> Also:
> 1. The first phase adversary $\mathcal A_\text{find}$'s output should have $|m_0| = |m_1|$.
> 2. In the chosen ciphertext attack setting, the second phase adversary $\mathcal A_\text{guess}$ is not allowed to query $c^*$ to the decryption oracle.

> [!definition] $(t,\varepsilon)$-IND-ATK security of a SKE
> A SKE scheme is **$(t, \varepsilon)$-IND-ATK secure** if for every adversary $\mathcal{A}$ that has running time bounded by $t$, we have:
> $$\text{Adv}_{\text{SKE}}^{\text{ind-atk}}(\mathcal A) \leq \varepsilon$$

> [!remark]
> 1. ATK here is a placeholder for the attacker. Unlike [[knowledge/cryptography/primitive/public-key encryption/Public Key Encryption#Indistinguishability\|PKE]], there is no public key, so even IND-CPA requires an explicit encryption oracle.
> 2. IND-EAV in bit-guessing form is exactly **semantic security** (Boneh–Shoup): $\text{SSadv}[\mathcal A, \mathcal E] = 2 \cdot \text{SSadv}^*[\mathcal A, \mathcal E]$, where $\text{SSadv}^*$ is the advantage above.
> 3. The multi-query (distinguishing) forms $\text{CPAadv}$ and $\text{CCAadv}$, where the adversary adaptively submits pairs $(m_{i0}, m_{i1})$ and must distinguish Experiment 0 from Experiment 1, are the versions used in the Construction theorems below; they relate to the bit-guessing form by a factor of 2.
> 4. 1CCA security restricts the adversary to a single encryption query; it is the notion used in [[knowledge/cryptography/primitive/message authentication/Authenticated Encryption\|Authenticated Encryption]].

> [!theorem] Semantic Security $\Rightarrow$ Message Recovery Security
> In the message recovery game, the challenger samples $m \xleftarrow{R} \mathcal M, k \xleftarrow{R} \mathcal K, c \xleftarrow{R} E(k, m)$ and the adversary outputs $\hat m$; define $\text{MRadv}[\mathcal A, \mathcal E] = \Pr[\hat m = m] - 1/|\mathcal M|$. If $\mathcal E$ is semantically secure, then $\text{MRadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

> [!theorem] Semantic Security $\Rightarrow$ Parity Prediction Security
> Let $\mathcal M = \{0, 1\}^L$. In the parity prediction game, the challenger acts as above and the adversary outputs $\hat b$; define $\text{Parityadv}[\mathcal A, \mathcal E] = |\Pr[\hat b = \text{parity}(m)] - 1/2|$. If $\mathcal E$ is semantically secure, then $\text{Parityadv}[\mathcal A, \mathcal E]$ is negligible for every efficient $\mathcal A$.

### Multi-key Semantic Security

> [!definition] SKE Multi-key Semantic Security Advantage
> For any adversary $\mathcal A$ and $b = 0, 1$, in Experiment $b$ the adversary submits queries $(m_{i0}, m_{i1}) \in \mathcal M^2$ of the same length ($i = 1, 2, \dots$); the challenger computes $k_i \leftarrow \text{Gen}(), c_i \leftarrow \text{Enc}(k_i, m_{ib})$ and returns $c_i$; finally the adversary outputs $\hat b \in \{0, 1\}$. Letting $W_b$ denote the event that $\hat b = 1$ in Experiment $b$, define:
> $$\text{Adv}_\text{SKE}^{\text{mss}}(\mathcal A) = |\Pr[W_0] - \Pr[W_1]|.$$

> [!definition] $(t,\varepsilon)$-Multi-key Semantic Security of a SKE
> A SKE scheme is **$(t, \varepsilon)$-multi-key semantically secure** if for every adversary $\mathcal{A}$ that has running time bounded by $t$, we have:
> $$\text{Adv}_{\text{SKE}}^{\text{mss}}(\mathcal A) \leq \varepsilon$$

> [!theorem]
> If $\mathcal E$ is semantically secure, it is multi-key semantically secure. For every MSS adversary $\mathcal A$ making at most $Q$ queries, there exists an SS adversary $\mathcal B$ ([[knowledge/cryptography/foundations/Elementary Wrapper\|elementary wrapper]]) such that $$\text{MSSadv}[\mathcal A, \mathcal E] = Q \cdot \text{SSadv}[\mathcal B, \mathcal E].$$

### Nonce-based CPA Security

> [!definition] SKE nCPA Advantage
> For a nonce-based cipher $\mathcal E$ defined over $(\mathcal K, \mathcal M, \mathcal C, \mathcal N)$, any adversary $\mathcal A$ and $b = 0, 1$, in Experiment $b$ the challenger selects $k \leftarrow \text{Gen}()$; the adversary submits queries $(m_{i0}, m_{i1}, n_i)$ with $|m_{i0}| = |m_{i1}|$ and $n_i \in \mathcal N \setminus \{n_1, \dots, n_{i-1}\}$; the challenger returns $c_i \leftarrow E(k, m_{ib}, n_i)$; finally the adversary outputs $\hat b \in \{0, 1\}$. Letting $W_b$ denote the event that $\hat b = 1$ in Experiment $b$, define:
> $$\text{Adv}_\text{SKE}^{\text{ncpa}}(\mathcal A) = |\Pr[W_0] - \Pr[W_1]|.$$

> [!definition] $(t,\varepsilon)$-nCPA security of a SKE
> A nonce-based SKE scheme is **$(t, \varepsilon)$-nCPA secure** if for every adversary $\mathcal{A}$ that has running time bounded by $t$, we have:
> $$\text{Adv}_{\text{SKE}}^{\text{ncpa}}(\mathcal A) \leq \varepsilon$$

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
