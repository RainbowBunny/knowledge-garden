---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/public-key-encryption/scheme/el-gamal-encryption/","dg-note-properties":{"aliases":["ElGamal Public Key Cryptosystem","Textbook ElGamal","ElGamal"]}}
---

Reference:
- `[Gal12]` — S. D. Galbraith, _Mathematics of Public Key Cryptography_ (CUP 2012), Ch. 20: §20.3 (textbook ElGamal, Figures 20.1 and 20.2), §20.4 (Theorems 20.4.2, 20.4.10, 20.4.11; Lemma 20.4.4; Example 20.4.7; Exercises 20.4.1, 20.4.5): https://www.math.auckland.ac.nz/~sgal018/crypto-book/ch20.pdf
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §8.4: Algorithms 8.17 and 8.18, Notes 8.21 and 8.23, §8.4.2: https://cacr.uwaterloo.ca/hac/about/chap8.pdf
- `[ElG85]` — T. ElGamal, _A Public Key Cryptosystem and a Signature Scheme Based on Discrete Logarithms_, IEEE Transactions on Information Theory 31, 469–472, 1985 — the original; not read.
- `[carried]` — kept from the previous version of this note, which followed Hoffstein, Pipher, Silverman, _An Introduction to Mathematical Cryptography_; not re-checked.

## Scheme

Reference Name: $\mathsf{ElGamal}$
Instantiates:: [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme\|Public-Key Encryption Scheme]]

> [!scheme] Setting
> - $\mathbb G$: a [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|Cyclic Group]] of prime order $q$ with generator $g$, written multiplicatively.
>
> `[Gal12 §20.3]` takes $\langle g \rangle$ inside an algebraic group over a finite field — $\mathbb F_p^*$, or an [[knowledge/math/algebra/structures/elliptic curve/Elliptic Curves over Finite Fields\|elliptic curve]]. `[HAC Alg 8.17]` takes all of $\mathbb Z_p^*$, whose order $p - 1$ is not prime — see Cryptanalysis.

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme\|Public-Key Encryption Scheme]]: Import $(\lambda, \mathrm{aux}, \mathcal M, \mathcal C, \mathcal R, \mathrm{pk}, \mathrm{sk})$, with
>     - $\mathrm{aux} = (\mathbb G, q, g)$.
>     - $\mathcal M = \mathbb G$.
>     - $\mathcal C = \mathbb G \times \mathbb G$.
>     - $\mathcal R = \{1, \dots, q - 1\}$.
> - $a \in \{1, \dots, q - 1\}$: the secret exponent.
> - $y = g^a$: the public element.
> - $r \in \mathcal R$: the encryption randomness, fresh for every message.

> [!scheme] ElGamal Encryption
> - $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: a public key $\mathrm{pk} = (\mathrm{aux}, y)$ and a secret key $\mathrm{sk} = (\mathrm{aux}, a)$.
>     - **Steps**:
>         1. Runs $\mathcal P(1^\lambda)$ for $\mathrm{aux} = (\mathbb G, q, g)$.
>         2. Samples $a \xleftarrow{\$} \{1, \dots, q - 1\}$.
>         3. Computes $y = g^a$.
>         4. Returns $(\mathrm{pk}, \mathrm{sk})$.
> - $c \leftarrow \mathsf{Enc}(\mathrm{pk}, m; r)$: (Randomized) Encryption algorithm.
>     - **Input**: a public key $\mathrm{pk} = (\mathrm{aux}, y)$, a message $m \in \mathbb G$, and randomness $r \in \mathcal R$.
>     - **Output**: a ciphertext $c = (c_1, c_2) \in \mathbb G \times \mathbb G$.
>     - **Steps**:
>         1. Samples $r \xleftarrow{\$} \mathcal R$, unless it is given.
>         2. Computes $c_1 = g^r$.
>         3. Computes $c_2 = m \cdot y^r$.
>         4. Returns $c = (c_1, c_2)$.
> - $m \leftarrow \mathsf{Dec}(\mathrm{sk}, c)$: (Deterministic) Decryption algorithm.
>     - **Input**: a secret key $\mathrm{sk} = (\mathrm{aux}, a)$ and a ciphertext $c = (c_1, c_2) \in \mathbb G \times \mathbb G$.
>     - **Output**: a message $m \in \mathbb G$.
>     - **Steps**:
>         1. Returns $m = c_2 \cdot c_1^{-a}$.
>
> `[Gal12 Fig 20.1]` `[HAC Alg 8.18]`

> [!remark] Notation in the literature
> | source | form | differences |
> | --- | --- | --- |
> | `[Gal12 Fig 20.1]` | $h = g^a$; $c_1 = g^k$, $c_2 = m h^k$ | the group order is $r$ and the randomness $k$; $\mathrm{pk} = (G, g, h)$, $\mathrm{sk} = a$ |
> | `[HAC Alg 8.17–8.18]` | $\alpha^a$; $(\gamma, \delta) = (\alpha^k, m (\alpha^a)^k)$ | $\alpha$ generates all of $\mathbb Z_p^*$; $1 \leq a, k \leq p - 2$; $\mathrm{pk} = (p, \alpha, \alpha^a)$, $\mathrm{sk} = a$; decryption computes $\gamma^{p - 1 - a} \delta$ |

## Property

### Correctness

> [!property] $\mathsf{ElGamal}$ Correctness `[HAC Alg 8.18]`
> $$c_2 \cdot c_1^{-a} = m \, y^r \, g^{-ar} = m \, g^{ar} g^{-ar} = m.$$

### Multiplicative homomorphism

> [!property] Ciphertexts multiply — the product of two ciphertexts encrypts the product of the messages
> Componentwise,
> $$(g^r, m \, y^r) \cdot (g^{r'}, m' \, y^{r'}) = (g^{r + r'},\ m m' \, y^{r + r'}),$$
> an encryption of $m m'$ with randomness $r + r'$. This is what makes the scheme malleable — see Cryptanalysis.

### Cost

- Encryption takes two exponentiations in $\mathbb G$, decryption one `[Gal12 §20.3]`.
- The ciphertext is two group elements for one: message expansion by a factor of $2$ `[HAC Note 8.21]`.

## Security

> [!security] One-way under passive attack iff CDH `[Gal12 Thm 20.4.2]`
> **Scope**
> - $\mathsf{ElGamal}$ over $\mathbb G$; an adversary that sees $\mathrm{pk}$ and one ciphertext.
>
> ---
> **Property**
> Recovering $m$ — [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme#One-wayness\|one-wayness]] under chosen-plaintext attack — is equivalent to the [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|CDH problem]] in $\mathbb G$.

> [!security] IND-CPA iff DDH `[Gal12 Thm 20.4.10]`
> **Scope**
> - $\mathsf{ElGamal}$ with message space $\mathcal M = \mathbb G = \langle g \rangle$.
>
> ---
> **Property**
> It is [[knowledge/cryptography/primitive/public-key encryption/property/Indistinguishability under Chosen-Plaintext Attack\|IND-CPA]] secure iff the [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|DDH problem]] is hard in $\mathbb G$.

> [!proof] Why DDH suffices
> The adversary sees $(y, c_1, c_2) = (g^a, g^r, m_b \, g^{ar})$, and $(g^a, g^r, g^{ar})$ is a DDH triple. Replace $g^{ar}$ by $g^z$ with $z$ uniform: $c_2 = m_b \, g^z$ is then uniform in $\mathbb G$ whatever $b$ is, so the adversary has advantage $0$. Any advantage in the real game is therefore an advantage in telling DDH triples from random ones.

## Cryptanalysis

> [!attack] Malleability — a decryption oracle decrypts every ciphertext `[Gal12 Lemma 20.4.4]`
> Given a target $c = (c_1, c_2)$, ask the oracle to decrypt $(c_1, c_2 \cdot g) \neq c$. It returns $m g$; divide by $g$. So $\mathsf{ElGamal}$ is not even one-way under an adaptive chosen-ciphertext attack, let alone IND-CCA; the hashed variant below fails in the same way `[Gal12 Ex 20.4.5]`.

> [!attack] Reusing the randomness `[HAC Note 8.23]`
> Two ciphertexts made with the same $r$ share $c_1$, and
> $$c_2 / c_2' = m / m',$$
> so whoever knows $m$ learns $m'$. A predictable $r$ — one drawn from a known linear congruential generator — also breaks the scheme `[Gal12 Ex 20.4.1]`.

> [!attack] The whole group $\mathbb F_p^*$ leaks a bit of the message `[Gal12 Ex 20.4.7]`
> If $g$ has odd prime order $q$ in $\mathbb F_p^*$, then $g$, $y$ and $y^r$ are squares, so the [[knowledge/complexity/problem/number/Quadratic Residue\|Legendre symbol]] of $c_2 = m y^r$ is that of $m$: if messages range over all of $\mathbb F_p^*$, one bit of $m$ is public, and IND-CPA fails. This is why $\mathcal M = \langle g \rangle$. With `[HAC]`'s generator $\alpha$ of all of $\mathbb Z_p^*$ the leak remains: the symbols of $\alpha^a$ and $\alpha^r$ are $(-1)^a$ and $(-1)^r$, which give $(-1)^{ar}$ and hence the symbol of $m$.

> [!attack] Public-key substitution — a man in the middle `[carried]`
> Eve replaces Alice's public element $y$ by her own $y_E = g^e$, decrypts Bob's ciphertext with $e$, and re-encrypts $m$ under $y$ for Alice, who notices nothing. Encryption needs an authentic public key — [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|Man-in-the-Middle Attack]].

## Variant

### Hashed ElGamal

> [!scheme] Semi-textbook ElGamal `[Gal12 Fig 20.2]`
> For a [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]] $H : \mathbb G \to \{0, 1\}^l$, with $\mathcal M = \{0, 1\}^l$ and the keys of $\mathsf{ElGamal}$:
> - $c \leftarrow \mathsf{Enc}(\mathrm{pk}, m; r)$: (Randomized) Encryption algorithm.
>     - **Input**: a public key $\mathrm{pk} = (\mathrm{aux}, y)$, a message $m \in \{0, 1\}^l$ and randomness $r \in \mathcal R$.
>     - **Output**: a ciphertext $c = (c_1, c_2) \in \mathbb G \times \{0, 1\}^l$.
>     - **Steps**:
>         1. Computes $c_1 = g^r$.
>         2. Computes $c_2 = m \oplus H(y^r)$.
>         3. Returns $c = (c_1, c_2)$.
> - $m \leftarrow \mathsf{Dec}(\mathrm{sk}, c)$: (Deterministic) Decryption algorithm.
>     - **Input**: a secret key $\mathrm{sk} = (\mathrm{aux}, a)$ and a ciphertext $c = (c_1, c_2)$.
>     - **Output**: a message $m \in \{0, 1\}^l$.
>     - **Steps**:
>         1. Returns $m = c_2 \oplus H(c_1^a)$.

> [!security] IND-CPA under CDH, in the random oracle model `[Gal12 Thm 20.4.11]`
> With $H$ modeled as a [[knowledge/cryptography/assumptions/idealized models/Random Oracle Model\|random oracle]], semi-textbook ElGamal is IND-CPA secure if CDH is hard. The version of `[BS]` with a symmetric cipher keyed by $H(g^r, y^r)$ is in [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme (Old)#ElGamal Encryption\|Public-Key Encryption Scheme (Old)#ElGamal Encryption]].

### Elliptic-curve ElGamal

> [!scheme] Elliptic-curve ElGamal
> $\mathsf{ElGamal}$ with $\mathbb G = \langle P \rangle \subseteq E(\mathbb F_p)$, written additively: $\mathrm{sk} = a$, $\mathrm{pk} = Y = aP$, and for a message point $M$:
> - $c \leftarrow \mathsf{Enc}(\mathrm{pk}, M; r)$: (Randomized) Encryption algorithm.
>     - **Input**: a public key $Y$, a message point $M \in \langle P \rangle$ and randomness $r$.
>     - **Output**: a ciphertext $c = (C_1, C_2)$, two points.
>     - **Steps**:
>         1. Computes $C_1 = rP$.
>         2. Computes $C_2 = M + rY$.
>         3. Returns $c = (C_1, C_2)$.
> - $M \leftarrow \mathsf{Dec}(\mathrm{sk}, c)$: (Deterministic) Decryption algorithm.
>     - **Input**: a secret key $a$ and a ciphertext $c = (C_1, C_2)$.
>     - **Output**: a message point $M$.
>     - **Steps**:
>         1. Returns $M = C_2 - a C_1$.
>
> `[Gal12 §20.3]` covers it, as $E$ is an algebraic group.

> [!remark] Practical difficulties `[carried]`
> - There is no obvious way to attach plaintext messages to points of $E(\mathbb F_p)$.
> - The message expansion is 4-to-1.

### Menezes–Vanstone variant

> [!scheme] Menezes–Vanstone `[carried]`
> Keys as in the elliptic-curve version; messages are pairs $(m_1, m_2) \in \mathbb F_p^2$, not points.
> - $c \leftarrow \mathsf{Enc}(\mathrm{pk}, (m_1, m_2); r)$: (Randomized) Encryption algorithm.
>     - **Input**: a public key $Y$, a message $(m_1, m_2) \in \mathbb F_p^2$ and randomness $r$.
>     - **Output**: a ciphertext $c = (R, c_1, c_2)$.
>     - **Steps**:
>         1. Computes $R = rP$.
>         2. Computes $(x_S, y_S) = rY$.
>         3. Returns $c = (R,\ x_S m_1 \bmod p,\ y_S m_2 \bmod p)$.
> - $(m_1, m_2) \leftarrow \mathsf{Dec}(\mathrm{sk}, (R, c_1, c_2))$: (Deterministic) Decryption algorithm.
>     - **Input**: a secret key $a$ and a ciphertext $(R, c_1, c_2)$.
>     - **Output**: a message $(m_1, m_2) \in \mathbb F_p^2$.
>     - **Steps**:
>         1. Computes $(x_S, y_S) = aR$.
>         2. Returns $(x_S^{-1} c_1 \bmod p,\ y_S^{-1} c_2 \bmod p)$.

## Related

### Constructions
- [[knowledge/cryptography/secure computation/Oblivious Transfer\|Oblivious Transfer]] — OT built from ElGamal ciphertexts that share their randomness

### Siblings
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]] — $c_1 = g^r$ is Bob's half of a Diffie–Hellman exchange with Alice's $y = g^a$, and $y^r = g^{ar}$ is the shared key that masks $m$
- [[knowledge/cryptography/primitive/digital signatures/scheme/ElGamal Signature\|ElGamal Signature]] — the same key pair, a different primitive

### Prerequisites
- [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|Computational Diffie-Hellman Assumption]], [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|Decisional Diffie-Hellman Assumption]], [[knowledge/complexity/problem/group/Discrete Logarithm Problem\|Discrete Logarithm Problem]]
