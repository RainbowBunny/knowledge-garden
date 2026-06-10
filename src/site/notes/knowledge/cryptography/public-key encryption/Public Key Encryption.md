---
{"dg-publish":true,"permalink":"/knowledge/cryptography/public-key-encryption/public-key-encryption/","dg-note-properties":{}}
---

## Syntax

> [!definition] Public Key Encryption Scheme
> A **public-key encryption scheme** $\text{PKE} = (\text{KeyGen}, \text{Enc}, \text{Dec})$ is a triple of efficient algorithms with a message space $\mathcal M$, ciphertext space $\mathcal C$, randomness space $\mathcal R$ and key space $\mathcal K$.
> - $(pk, sk) \leftarrow \text{KeyGen}()$: The key-generation algorithm $\text{KeyGen}$ returns a pair $(pk, sk)$ consisting of a public key $pk$ and a secret key $sk$. 
> - $c \leftarrow \text{Enc}(pk, m)$ (Deterministic) or $c \leftarrow \text{Enc}(pk, m; r)$ (Probabilistic): The encryption algorithm takes a public key $pk$, a message $m \in \mathcal M$ and possibly an internal random $r \leftarrow \mathcal R$ to produce a ciphertext $c \in \mathcal C$.
> - $m \leftarrow \text{Dec}(sk, c)$: The deterministic decryption algorithm takes a secret key $sk$ and a ciphertext $c$, and outputs either a message $m \in \mathcal M$ or a special symbol $\perp$ to indicate **rejection**. 

> [!algorithm] Public-key Encryption Scheme (Mathematical Detail)
> A **public-key encryption scheme** consists of three algorithms, $G$, $E$, and $D$, along with two families of spaces with system parameterization $P$: 
> $$M = \{\mathcal M_{\lambda, \Lambda}\}_{\lambda, \Lambda} \quad \text{and} \quad C = \{\mathcal C_{\lambda, \Lambda}\}_{\lambda, \Lambda},$$
> such that
> 1. $M$ and $C$ are efficiently recognizable.
> 2. $M$ has an effective length function.
> 3. Algorithm $G$ is an efficiently probabilistic algorithm that on input $\lambda, \Lambda$, where $\lambda \in \mathbb Z_{\geq 1}, \Lambda \in \text{Supp}(P(\lambda))$, outputs a pair $(pk, sk)$, where $pk$ and $sk$ are bit strings whose lengths are always bounded by a polynomial in $\lambda$.
> 4. Algorithm $E$ is an efficiently probabilistic algorithm that on input $\lambda, \Lambda, pk, m$, where $\lambda \in \mathbb Z_{\geq 1}, \Lambda \in \text{Supp}(P(\lambda)), (pk, sk) \in \text{Supp}(G(\lambda, \Lambda))$ for some $sk$, and $m \in \mathcal M_{\lambda, \Lambda}$, always outputs an element of $\mathcal C_{\lambda, \Lambda}$.
> 5. Algorithm $D$ is an efficiently deterministic algorithm that on input $\lambda, \Lambda, sk, c$, where $\lambda \in \mathbb Z_{\geq 1}, \Lambda \in \text{Supp}(P(\lambda)), (pk, sk) \in \text{Supp}(G(\lambda, \Lambda))$ for some $pk$, and $c \in \mathcal C_{\lambda, \Lambda}$, outputs either an element of $\mathcal M_{\lambda, \Lambda}$, or a special symbol $\text{reject} \notin \mathcal M_{\lambda, \Lambda}$.
> 6. For all $\lambda, \Lambda, pk, sk, m, c$, where $\lambda \in \mathbb Z_{\geq 1}, \Lambda \in \text{Supp}(P(\lambda)), (pk, sk) \in \text{Supp}(G(\lambda, \Lambda)), k \in \mathcal K_{\lambda, \Lambda}, m \in \mathcal M_{\lambda, \Lambda}$ and $c \in \text{Supp}(E(\lambda, \Lambda; pk, m))$, we have $D(\lambda, \Lambda; sk, c) = m$.

## Property

### Injectivity

> [!definition] PKE Injectivity
> A public-key encryption scheme $\text{PKE}$ is *injective* if for all key pairs $(pk, sk) \leftarrow \text{Gen}()$, it holds that $\text{Enc}(pk, m; r) = \text{Enc}(pk, m'; r') \Rightarrow (m, r) = (m', r')$ for all $m, m' \in \mathcal M$ and $r, r' \in \mathcal R$.

### Correctness

> [!definition] PKE $(1-\delta)$-Correctness
> A public-key encryption scheme $\text{PKE}$ is $(1-\delta)$-correct if 
> $$E[\max_{m \in \mathcal M} \Pr[\text{Dec}(sk, \text{Enc}(pk, m)) = m]] \geq 1 - \delta$$

> [!remark]
> For some literature, this definition comes from the decryption failure rate and thus we have the following correctness definition. So in writing please use the above definition instead.

### Min-Entropy

> [!definition] Min-Entropy
> Given $(pk, sk) \in \mathcal K, m \in \mathcal M$, we define the **min-entropy** of $\text{Enc}(pk, m)$ by 
> $$\gamma(pk, m) = -\log \max_{c \in \mathcal C} \Pr[c = \text{Enc}(pk, m; r) \; | \; r \in \mathcal R].$$
> We say that a $\text{PKE}$ is $\gamma$**-spread** if: 
> $$\forall (pk, sk) \in \mathcal K, m \in \mathcal M, c \in \mathcal C: \gamma(pk, m) \geq \gamma$$

> [!corollary]
> For every ciphertext $c \in \mathcal C$, we have 
> $$\Pr[c = \text{Enc}(pk, m; r) \; | \; r \leftarrow \mathcal R] \leq 2^{-\gamma}$$

### Rigidity

> [!definition] PKE Rigidity
> We say that a $\text{PKE}$ is **rigid** if for all key pairs $(pk, sk) \leftarrow Gen()$, and all ciphertexts $c$, it holds that either $\text{Dec}(sk, c) = \perp$ or $\text{Enc}(pk, \text{Dec}(sk, c)) = c$.

## Security

### Indistinguishability

> [!definition] PKE Indistinguishability Advantage
> For any adversary $\mathcal A = (\mathcal A_\text{find}, \mathcal A_\text{guess})$, we define the indistinguiability advantage:
> $$\text{Adv}_\text{PKE}^{\text{ind-atk}}(\mathcal A) = 
> \left|\; \Pr\!\left[ b = b' \;\middle |\; 
> \begin{array}{l}
> (pk, sk) \leftarrow \text{KeyGen}(); \\
> (m_0, m_1, s) \leftarrow \mathcal A_\text{find}^{\mathcal O_\text{find}}(pk); \\
> b \xleftarrow{\$} \{0, 1\}; c^* \leftarrow \text{Enc}(pk, m_b); \\
> b' \leftarrow \mathcal A_\text{guess}^{\mathcal O_\text{guess}}(s, c^*)
> \end{array} \right] 
> \;- \frac{1}{2}
> \right|.$$
> Where:
> 1. Chosen Ciphertext Attack: $\text{atk} = \text{cca}$ then $\mathcal O_\text{find}(\cdot) = \varepsilon$ and $\mathcal O_\text{guess}(\cdot) = \varepsilon$.
> 2. Lunch Time Attack: $\text{atk} = \text{lta}$ then $\mathcal O_\text{find}(\cdot) = \text{Dec}(sk, \cdot)$ and $\mathcal O_\text{guess}(\cdot) = \varepsilon$.
> 3. Adaptive Chosen Ciphertext Attack: $\text{atk} = \text{cca}$ then $\mathcal O_\text{find}(\cdot) = \text{Dec}(sk, \cdot)$ and $\mathcal O_\text{guess}(sk, \cdot)$
> 
> Also:
> 1. The first phase adversary $\mathcal A_\text{find}$'s output should have $|m_0| = |m_1|$.
> 2. In the adaptive chosen ciphertext attack setting, the second phase adversary $\mathcal A_2$ is not allowed to query $c^*$ to the oracle.

> [!definition] $(t,\varepsilon)$-IND-ATK security of a PKE 
> A PKE scheme is **$(t, \varepsilon)$-IND-ATK secure** if for every adversary $\mathcal{A}$ that has running time bounded by $t$, we have: 
> $$\text{Adv}_{\text{PKE}}^{\text{ind-atk}}(\mathcal A) \leq \varepsilon$$

> [!remark]
> 1. ATK here is a placeholder for the attacker.
> 2. Lunch time attack means that only one phase (before lunch) for oracle.

 > [!security]
 > If a public-key encryption scheme $\mathcal E$ is semantically secure, then it is also CPA secure.
 > 
 > In particular, for every [[knowledge/cryptography/public-key encryption/Public Key Encryption#Chosen Plaintext Attack Security\|CPA security]] adversary $\mathcal A$ with respect to $\mathcal E$, and which makes at most $Q$ queries to its challenger, there exists an [[knowledge/cryptography/public-key encryption/Public Key Encryption#Semantic Security\|semantic security]] adversary $\mathcal B$, where $\mathcal B$ is an elementary wrapper around $\mathcal A$, such that 
 > $$\text{CPAadv}[\mathcal A, \mathcal E] = Q \cdot \text{SSadv}[\mathcal B, \mathcal E].$$

### Non-Malleability

> [!definition] PKE Non-Malleability Advantage
> For any adversary $\mathcal A = (\mathcal A_\text{find}, \mathcal A_\text{maul})$, we define the non-malleability advantage:
> $$\text{Adv}_\text{PKE}^{\text{nm-atk}}(\mathcal A) = 
>  
> \left|\; \Pr\!\left[
> \begin{array}{l}
> c \notin (c_1, \dots, c_n) \; \\ 
> \perp \; \notin (m_1, \dots, m_n) \\ 
> R(m, (m_1, \dots, m_n))
> \end{array}
> \;\middle |\; 
> \begin{array}{l}
> (pk, sk) \leftarrow \text{KeyGen}(); \\
> (M, s) \leftarrow \mathcal A_\text{find}^{\mathcal O_\text{find}}(pk); \\
> m \leftarrow M; c \leftarrow \text{Enc}(pk, m) \\
> (R, (c_1, \dots, c_n)) \leftarrow \mathcal A_\text{maul}^{\mathcal O_\text{maul}} (M, s, c); \\
> (m_1, \dots, m_n) \leftarrow \text{Dec}(sk, (y_1, \dots, y_n)))
> \end{array} \right] 
> \;- 
> \Pr\!\left[
> \begin{array}{l}
> c \notin (c_1, \dots, c_n) \; \\ 
> \perp \; \notin (m_1, \dots, m_n) \\ 
> R(\tilde m, (m_1, \dots, m_n))
> \end{array}
> \;\middle |\; 
> \begin{array}{l}
> (pk, sk) \leftarrow \text{KeyGen}(); \\
> (M, s) \leftarrow \mathcal A_\text{find}^{\mathcal O_\text{find}}(pk); \\
> m, \tilde m \leftarrow M; c \leftarrow \text{Enc}(pk, m) \\
> (R, (c_1, \dots, c_n)) \leftarrow \mathcal A_\text{maul}^{\mathcal O_\text{maul}} (M, s, c); \\
> (m_1, \dots, m_n) \leftarrow \text{Dec}(sk, (y_1, \dots, y_n)))
> \end{array} \right] 
> \right|.$$
> Where:
> 1. Chosen Ciphertext Attack: $\text{atk} = \text{cca}$ then $\mathcal O_\text{find}(\cdot) = \varepsilon$ and $\mathcal O_\text{guess}(\cdot) = \varepsilon$.
> 2. Lunch Time Attack: $\text{atk} = \text{lta}$ then $\mathcal O_\text{find}(\cdot) = \text{Dec}(sk, \cdot)$ and $\mathcal O_\text{guess}(\cdot) = \varepsilon$.
> 3. Adaptive Chosen Ciphertext Attack: $\text{atk} = \text{cca}$ then $\mathcal O_\text{find}(\cdot) = \text{Dec}(sk, \cdot)$ and $\mathcal O_\text{guess}(sk, \cdot)$
> 
> Also:
> 1. $R$ is a predicate.

> [!definition] $(t,\varepsilon)$-NM-ATK security of a PKE 
> A PKE scheme is **$(t, \varepsilon)$-NM-ATK secure** if for every adversary $\mathcal{A}$ that has running time bounded by $t$, we have: 
> $$\text{Adv}_{\text{PKE}}^{\text{nm-atk}}(\mathcal A) \leq \varepsilon$$

### One-way Encryption

> [!definition] PKE OWE Advantage
> For any adversary $\mathcal A$, we define the OWE advantage:
> $$\text{Adv}_{\text{PKE}}^{\text{owe}}(\mathcal A) = 
> \; \Pr\!\left[ \mathcal A(pk, c) = \text{Dec}(sk, c) \; \middle | \; 
> \begin{array}{l}
> (pk, sk) \leftarrow \text{KeyGen}(); \\
> m \leftarrow \mathcal M; \\
> c \leftarrow \text{Enc}(pk, m)
> \end{array} \right]$$

> [!definition] $(t,\varepsilon)$-OWE security of a PKE 
> A PKE scheme is **$(t, \varepsilon)$-OWE secure** if for every adversary $\mathcal{A}$ that has running time bounded by $t$, we have: 
> $$\text{Adv}_{\text{PKE}}^{\text{owe}}(\mathcal A) \leq \varepsilon$$

### One-Wayness under Chosen Plaintext Attacks

> [!definition] PKE OWE-CPA Advantage
> For any adversary $\mathcal A$, we define the OWE-CPA advantage:
> $$\text{Adv}_\text{PKE}^{\text{owe-cpa}}$$

## Construction

### Based on a Trapdoor Function Scheme

> [!algorithm] PKE by Trapdoor Function Scheme
> Component of $\mathcal E_{TDF}$:
> - A trapdoor function scheme $\mathcal T = (G, F, I)$, defined over $(\mathcal X, \mathcal Y)$,
> - A symmetric cipher $\mathcal E_s = (E_s, D_s)$, defined over $(\mathcal K, \mathcal M, \mathcal C)$,
> - A hash function $H: \mathcal X \rightarrow \mathcal K$.
> 
> Message space for $\mathcal E_{TDF}$ is $\mathcal M$, ciphertext space is $\mathcal Y \times \mathcal C$.
> - The key generation algorithm for $\mathcal E_{TDF}$ is the key generation algorithm for $\mathcal T$.
> - For a given public key $pk$, and a given message $m \in \mathcal M$, the encryption algorithm runs as follows: 
> $$E(pk, m) = x \xleftarrow{R} \mathcal X, y \leftarrow F(pk, x), k \leftarrow H(x), c \xleftarrow{R} E_s(k, m), \text{output } (y, c)$$
> - For a given secret key $sk$, and a given ciphertext $(y, c) \in \mathcal Y \times \mathcal C$, the decryption algorithm runs as follows: 
> $$D(sk, (y, c)) = x \leftarrow I(sk, y), k \leftarrow H(x), m \leftarrow D_s(k, c), \text{output } m.$$
> 
> Thus $\mathcal E_{TDF} = (G, E, D)$, and is defined over $(\mathcal M, \mathcal Y \times \mathcal C)$.

> [!theorem] 
> Assume $H: \mathcal X \rightarrow \mathcal K$ is modeled as a random oracle. If $\mathcal T$ is one-way and $\mathcal E_s$ is semantically secure, then $\mathcal E_{TDF}$ is semantically secure.
> 
> In particular, for every [[knowledge/cryptography/public-key encryption/Public Key Encryption#Semantic Security\|semantic security]] adversary $\mathcal A$ that attacks $\mathcal E_{TDF}$, there exists an [[knowledge/cryptography/public-key encryption/Public Key Encryption#One-way Security\|inverting]] adversary $\mathcal B_{ow}$ that attacks $\mathcal T$, and an [[knowledge/cryptography/public-key encryption/Public Key Encryption#Semantic Security\|semantic security]] adversary $\mathcal B_s$ that attacks $\mathcal E_s$, where $\mathcal B_{ow}$ and $\mathcal B_s$ are elementary wrappers around $\mathcal A$, such that 
> $$\text{SS}^{ro}\text{adv}[\mathcal A, \mathcal E_{TDF}] \leq 2 \cdot \text{OWadv}[\mathcal B_{ow}, \mathcal T] + \text{SSadv}[\mathcal B_s, \mathcal E_s]$$

## Case Study

### RSA Trapdoor Function Scheme

> [!algorithm] RSA Trapdoor Function Scheme
> The basic RSA encryption scheme is $\mathcal E_{RSA} = (G, E, D)$, with message space $\mathcal M$ and ciphertext space $\mathcal X \times \mathcal C$, where
> - The key generation algorithm runs as follows: 
> $$G() = (n, d) \xleftarrow{R} \text{RSAGen}(\ell, e), pk \leftarrow (n, e), sk \leftarrow (n, d), \text{output } (pk, sk);$$
> - For a given public key $pk = (n, e)$, and message $m \in \mathcal M$, the encryption algorithm runs as follows: 
> $$E(pk, m) = x \xleftarrow{R} \mathbb Z_n, y \leftarrow x^e, k \leftarrow H(x), c \xleftarrow{R} E_s(k, m), \text{output } (y, c) \in \mathcal X \times \mathcal C'$$
> - For a given secret key $sk = (n, d)$, and a given ciphertext $(y, c) \in \mathcal X \times \mathcal C$, where $y$ represents an element of $\mathbb Z_n$, the decryption algorithm runs as follows: 
> $$D(sk, (y, c)) = x \leftarrow y^d, k \leftarrow H(x), m \leftarrow D_s(k, c), \text{output } m.$$

> [!theorem]
> Assume $H : \mathcal X \rightarrow \mathcal K$ is modeled as a random oracle. If the RSA assumption holds for parameters $(\ell, e)$, and $\mathcal E_s$ is semantically secure, then $\mathcal E_{RSA}$ is semantically secure.
> 
> In particular, for any [[knowledge/cryptography/public-key encryption/Public Key Encryption#Semantic Security\|semantic security]] $\mathcal A$ that attacks $\mathcal E_{RSA}$, there exist an RSA adversary $\mathcal B_{rsa}$ that breaks the [[knowledge/cryptography/special functions/Trapdoor Functions#A Trapdoor Permutation Scheme Based on RSA\|RSA assumption]] for $(\ell, e)$, and an [[knowledge/cryptography/public-key encryption/Public Key Encryption#Semantic Security\|semantic security]] adversary $\mathcal B_s$ that attacks $\mathcal E_s$, where $\mathcal B_{rsa}$ and $\mathcal B_s$ are elementary wrappers around $\mathcal A$, such that 
> $$\text{SS}^{ro}\text{adv}^*[\mathcal A, \mathcal E_{RSA}] \leq \text{RSAadv}[\mathcal B_{RSA}, \ell, e] + \text{SSadv}^*[\mathcal B_s, \mathcal E_s].$$

### ElGamal Encryption

> [!algorithm] ElGamal Encryption
> Components of ElGamal encryption:
> - A cyclic group $\mathbb G$ of prime order $q$ with generator $g \in \mathbb G$,
> - A symmetric cipher $\mathcal E_s = (E_s, D_s)$, defined over $(\mathcal K, \mathcal M, \mathcal C)$,
> - A hash function $H: \mathbb G^2 \rightarrow \mathcal K$.
> The key generation, encryption, and decryption algorithms for $\mathcal E_{EG}$.
> - The key generation algorithm runs as follows: 
> $$\begin{align} G() = \quad &\alpha \xleftarrow{R} \mathbb Z_q, u \leftarrow g^\alpha, \\ &pk \leftarrow u, sk \leftarrow \alpha \\ &\text{output }(pk, sk); \end{align}$$
> - For a given public key $pk = u \in \mathbb G$ and message $m \in \mathcal M$, the encryption algorithm runs as follows:
> $$E(pk, m) = \beta \xleftarrow{R} \mathbb Z_q, v \leftarrow g^\beta, w \leftarrow u^\beta, k \leftarrow H(v, w), c \leftarrow E_s(k, m), \text{output } (v, c);$$
> - For a given secret key $sk = \alpha \in \mathbb Z_q$ and a ciphertext $(v, c) \in \mathbb G \times \mathcal C$, the decryption algorithm runs as follows: 
> $$D(sk, (v, c)) = w \leftarrow v^\alpha, k \leftarrow H(v, w), m \leftarrow D_s(k, c), \text{output } m.$$
> 
> Thus, $\mathcal E_{EG} = (G, E, D)$, and is defined over $(\mathcal M, \mathbb G \times \mathcal C)$.

> [!theorem]
> Assume $H: \mathbb G^2 \rightarrow \mathcal K$ is modeled as a random oracle. If the CDH assumption holds for $\mathbb G$, and $\mathcal E_s$ is semantically secure, then $\mathcal E_{EG}$ is semantically secure.
> 
> In particular, for every [[knowledge/cryptography/public-key encryption/Public Key Encryption#Semantic Security\|semantic security]] adversary $\mathcal A$ with respect to $\mathcal E_{EG}$, and makes at most $Q$ queries to the random oracle, there exist a [[knowledge/cryptography/key establishment/key exchange/Key Exchange#Computational Diffie-Hellman\|computational Diffie-Hellman]] adversary $\mathcal B_{cdh}$ with respect to $\mathbb G$, and an [[knowledge/cryptography/public-key encryption/Public Key Encryption#Semantic Security\|semantic security]] adversary $\mathcal B_s$ with respect to $\mathcal E_s$, where $\mathcal B_{cdh}$ and $\mathcal B_s$ are elementary wrappers around $\mathcal A$, such that 
> $$\text{SS}^{ro}\text{adv}[\mathcal A, \mathcal E_{EG}] \leq 2Q \cdot \text{CDHadv}[\mathcal B_{cdh}, \mathbb G] + \text{SSadv}[\mathcal B_s, \mathcal E_s].$$

### Lattice-Based Instantiation

> [!algorithm] Lattice-Based Instatiation
> - $\text{Setup}$
> 	- $\tau$: $\ell_{\infty}$-norm bound on all short elements in the scheme.
> 	- $q_{PKE}$: a modulus
> 	- $p < q_{PKE}$: a positive integer
> - $\text{KeyGen}()$:
> 	- Sample $A_1 \in \mathcal R_{128}^{8 \times 8}$ uniform modulo $q_{PKE}$.
> 	- Sample $S_1, S_2 \leftarrow U(\mathcal S_r^{12 \times 8})$.
> 	- Compute $A_2 = S_1 \cdot A_1 + S_2$
> 	- Set $pk = (A_1, A_2)$ and $sk = S_1$
> - $\text{Enc}(pk = (A_1, A_2), m \in \mathcal R_{128}^{12})$
> 	- Sample $s, e_1 \leftarrow U(\mathcal S_\tau^8)$, and $e_2 \leftarrow U(\mathcal S_{\tau}^{12})$
> 	- Compute $c_1 = A_1 \cdot s + e_1$
> 	- Compute $c_2 = A_2 \cdot s + e_2 + p \cdot m$
> 	- Return $ct = (c_1, c_2)$.
> - $\text{Dec}(sk = S_1, ct = (c_1, c_2))$
> 	- Compute $t = c_2 - S_1 \cdot c_1$
> 	- Return $(t - t \mod p) / p$.



