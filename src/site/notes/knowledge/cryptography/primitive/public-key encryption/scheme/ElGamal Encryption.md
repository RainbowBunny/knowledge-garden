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

### Setting

> [!scheme] Setting
> - $G$: a finite group, written multiplicatively, and $g \in G$ of prime order $r$; $\langle g \rangle$ is a [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|cyclic group]] of order $r$.
>
> `[Gal12 §20.3]` takes $G$ to be an algebraic group over a finite field — $\mathbb F_p^*$, or an [[knowledge/math/algebra/structures/elliptic curve/Elliptic Curves over Finite Fields\|elliptic curve]] — with $r$ a prime divisor of $\# G$. `[HAC Alg 8.17]` takes $G = \mathbb Z_p^*$ with $g$ a generator of the whole group, and `[HAC §8.4.2]` any finite cyclic group.

### Parameters

> [!definition] Parameters
> - $r$: the prime order of $g$.
> - $\mathcal M = \langle g \rangle$: the messages. $\langle g \rangle \times \langle g \rangle$: the ciphertexts.
> - $a$: the secret key, $0 < a < r$. $h = g^a$: the public key.
> - $k$: the encryption randomness, $0 < k < r$, fresh for every message.

### Algorithms

> [!scheme] Algorithms
> - $(\mathrm{pk}, a) \leftarrow \mathsf{KeyGen}(G, g, r)$: (Randomized) Key-generation algorithm.
>     - **Output**: a secret key $a$ and the public key $\mathrm{pk} = (G, g, h)$.
>     - **Steps**: $a \xleftarrow{\$} \{1, \dots, r - 1\}$; $h = g^a$.
> - $(c_1, c_2) \leftarrow \mathsf{Enc}(\mathrm{pk}, m)$: (Randomized) Encryption algorithm.
>     - **Input**: the public key and a message $m \in \langle g \rangle$.
>     - **Output**: a ciphertext $(c_1, c_2) \in \langle g \rangle^2$.
>     - **Steps**: $k \xleftarrow{\$} \{1, \dots, r - 1\}$; $c_1 = g^k$; $c_2 = m \cdot h^k$.
> - $m \leftarrow \mathsf{Dec}(a, (c_1, c_2))$: (Deterministic) Decryption algorithm.
>     - **Steps**: returns $m = c_2 \cdot c_1^{-a}$.
>
> `[Gal12 Fig 20.1]` `[HAC Alg 8.18]`

> [!remark] Notation in the literature
> | source | generator | keys | ciphertext |
> | --- | --- | --- | --- |
> | `[Gal12 Fig 20.1]` | $g$ of prime order $r$ | $a$, $h = g^a$ | $(c_1, c_2)$ |
> | `[HAC Alg 8.17–8.18]` | $\alpha$, generator of $\mathbb Z_p^*$ | $a$, $\alpha^a$ | $(\gamma, \delta)$ |

## Property

### Correctness

> [!property] ElGamal Correctness `[HAC Alg 8.18]`
> $$c_2 \cdot c_1^{-a} = m \, h^k \, g^{-ak} = m \, g^{ak} g^{-ak} = m.$$

### Multiplicative homomorphism

> [!property] Ciphertexts multiply — the product of two ciphertexts encrypts the product of the messages
> Componentwise,
> $$(g^k, m \, h^k) \cdot (g^{k'}, m' \, h^{k'}) = (g^{k + k'},\ m m' \, h^{k + k'}),$$
> an encryption of $m m'$ with randomness $k + k'$. This is what makes the scheme malleable — see Cryptanalysis.

### Cost

- Encryption takes two exponentiations in $G$, decryption one `[Gal12 §20.3]`.
- The ciphertext is two group elements for one: message expansion by a factor of $2$ `[HAC Note 8.21]`.

## Security

> [!security] One-way under passive attack iff CDH `[Gal12 Thm 20.4.2]`
> **Scope**
> - Textbook ElGamal over $\langle g \rangle$; an attacker that sees $\mathrm{pk}$ and $(c_1, c_2)$ only.
>
> ---
> **Property**
> Recovering $m$ — [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme#One-wayness\|one-wayness]] under chosen-plaintext attack — is equivalent to the [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|CDH problem]] in $\langle g \rangle$.

> [!security] IND-CPA iff DDH `[Gal12 Thm 20.4.10]`
> **Scope**
> - Textbook ElGamal with message space $\mathcal M = \langle g \rangle$.
>
> ---
> **Property**
> It is [[knowledge/cryptography/primitive/public-key encryption/property/Indistinguishability under Chosen-Plaintext Attack\|IND-CPA]] secure iff the [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|DDH problem]] is hard in $\langle g \rangle$.

> [!proof] Why DDH suffices
> The adversary sees $(h, c_1, c_2) = (g^a, g^k, m_b \, g^{ak})$, and $(g^a, g^k, g^{ak})$ is a DDH triple. Replace $g^{ak}$ by $g^z$ with $z$ uniform: $c_2 = m_b \, g^z$ is then uniform in $\langle g \rangle$ whatever $b$ is, so the adversary has advantage $0$. Any advantage in the real game is therefore an advantage in telling DDH triples from random ones.

## Cryptanalysis

> [!attack] Malleability — a decryption oracle decrypts every ciphertext `[Gal12 Lemma 20.4.4]`
> Given a target $(c_1, c_2)$, ask the oracle to decrypt $(c_1, c_2 \cdot g) \neq (c_1, c_2)$. It returns $m g$; divide by $g$. So textbook ElGamal is not even one-way under an adaptive chosen-ciphertext attack, let alone IND-CCA; the hashed variant below fails in the same way `[Gal12 Ex 20.4.5]`.

> [!attack] Reusing the randomness `[HAC Note 8.23]`
> Two ciphertexts made with the same $k$ share $c_1$, and
> $$c_2 / c_2' = m / m',$$
> so whoever knows $m$ learns $m'$. A predictable $k$ — one drawn from a known linear congruential generator — also breaks the scheme `[Gal12 Ex 20.4.1]`.

> [!attack] The whole group $\mathbb F_p^*$ leaks a bit of the message `[Gal12 Ex 20.4.7]`
> If $g$ has odd prime order $r$ in $\mathbb F_p^*$, then $g$, $h$ and $h^k$ are squares, so the [[knowledge/complexity/problem/number/Quadratic Residue\|Legendre symbol]] of $c_2 = m h^k$ is that of $m$: if messages range over all of $\mathbb F_p^*$, one bit of $m$ is public, and IND-CPA fails. This is why messages are restricted to $\langle g \rangle$ of prime order. With `[HAC]`'s generator $\alpha$ of all of $\mathbb Z_p^*$ the leak remains: the symbols of $\alpha^a$ and $\gamma$ are $(-1)^a$ and $(-1)^k$, which give $(-1)^{ak}$ and hence the symbol of $m$.

> [!attack] Public-key substitution — a man in the middle `[carried]`
> Eve replaces Alice's public key $h$ by her own $h_E = g^e$, decrypts Bob's ciphertext with $e$, and re-encrypts $m$ under $h$ for Alice, who notices nothing. Encryption needs an authentic public key — [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|Man-in-the-Middle Attack]].

## Variant

### Hashed ElGamal

> [!scheme] Semi-textbook ElGamal `[Gal12 Fig 20.2]`
> For a hash function $H : G \to \{0, 1\}^l$ and $m \in \{0, 1\}^l$:
> $$c_1 = g^k, \qquad c_2 = m \oplus H(h^k), \qquad m = c_2 \oplus H(c_1^a).$$

> [!security] IND-CPA under CDH, in the random oracle model `[Gal12 Thm 20.4.11]`
> With $H$ modeled as a [[knowledge/cryptography/assumptions/idealized models/Random Oracle Model\|random oracle]], semi-textbook ElGamal is IND-CPA secure if CDH is hard. The version of `[BS]` with a symmetric cipher keyed by $H(g^k, h^k)$ is in [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme (Old)#ElGamal Encryption\|Public-Key Encryption Scheme (Old)#ElGamal Encryption]].

### Elliptic-curve ElGamal

> [!scheme] Elliptic-curve ElGamal
> The same scheme in $G = E(\mathbb F_p)$, written additively, with a base point $P$, secret $n_A$ and public key $Q_A = n_A P$:
> $$C_1 = kP, \qquad C_2 = M + k Q_A, \qquad M = C_2 - n_A C_1,$$
> for a message point $M \in E(\mathbb F_p)$. `[Gal12 §20.3]` covers it, as $E$ is an algebraic group.

> [!remark] Practical difficulties `[carried]`
> - There is no obvious way to attach plaintext messages to points of $E(\mathbb F_p)$.
> - The message expansion is 4-to-1.

### Menezes–Vanstone variant

> [!scheme] Menezes–Vanstone `[carried]`
> Messages are pairs $(m_1, m_2) \in \mathbb F_p^2$, not points. With $R = kP$ and $kQ_A = (x_S, y_S)$, the ciphertext is
> $$(R,\ c_1 = x_S m_1 \bmod p,\ c_2 = y_S m_2 \bmod p);$$
> Alice computes $n_A R = (x_S, y_S)$ and returns $m_1 = x_S^{-1} c_1$, $m_2 = y_S^{-1} c_2$.

## Related

### Constructions
- [[knowledge/cryptography/secure computation/Oblivious Transfer\|Oblivious Transfer]] — OT built from ElGamal ciphertexts that share their randomness

### Siblings
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]] — $c_1 = g^k$ is Bob's half of a Diffie–Hellman exchange with Alice's $h = g^a$, and $h^k = g^{ak}$ is the shared key that masks $m$
- [[knowledge/cryptography/primitive/digital signatures/scheme/ElGamal Signature\|ElGamal Signature]] — the same keys, a different primitive

### Prerequisites
- [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|Computational Diffie-Hellman Assumption]], [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|Decisional Diffie-Hellman Assumption]], [[knowledge/complexity/problem/group/Discrete Logarithm Problem\|Discrete Logarithm Problem]]
