---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/key-establishment/key-exchange/scheme/diffie-hellman-key-exchange/","dg-note-properties":{"aliases":["DH","Diffie-Hellman"]}}
---

Reference:
- `[DH76]` — W. Diffie, M. E. Hellman, _New Directions in Cryptography_, IEEE Transactions on Information Theory IT-22(6), 1976, pp. 644–654, §III (public key distribution): http://www-ee.stanford.edu/%7Ehellman/publications/24.pdf
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, §10.4. Copy of Ch. 10: https://www.cis.upenn.edu/~sga001/classes/cis331f19/resources/bs_ch10.pdf
- `[Gal12]` — S. D. Galbraith, _Mathematics of Public Key Cryptography_ (CUP 2012), Ch. 20: §20.1, §20.2.1, §20.5: https://www.math.auckland.ac.nz/~sgal018/crypto-book/ch20.pdf
- `[CK01]` — R. Canetti, H. Krawczyk, _Analysis of Key-Exchange Protocols and Their Use for Building Secure Channels_, EUROCRYPT 2001, §4.1 (protocol 2DH, Theorem 2): https://www.iacr.org/archive/eurocrypt2001/20450451.pdf
- `[Cia24]` — M. Ciampi, _Introduction to Modern Cryptography_, Lecture 13 (Key Exchange and the Diffie-Hellman Protocol), University of Edinburgh, slides citing Katz–Lindell §10.3–10.4: https://opencourse.inf.ed.ac.uk/sites/default/files/https/opencourse.inf.ed.ac.uk/imc/2024/diffie-hellman.pdf
- `[HPS]` — J. Hoffstein, J. Pipher, J. H. Silverman, _An Introduction to Mathematical Cryptography_ (2nd ed., Springer 2014) — the presentation the tripartite section follows; not opened.
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Scheme

Reference Name: $\mathsf{DH}$
Instantiates:: [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]]

### Setting

> [!scheme] Setting
> - $\mathbb G$: a [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|Cyclic Group]] of prime order $q$ with generator $g$ — `[Gal12 §20.2.1]` allows any algebraic group, elliptic curves included (§20.1).

### Parties

> [!definition] Parties
> - Alice and Bob, who run the protocol.
> - The description of $\mathbb G$, $g$ and $q$ is a system parameter, generated once at setup and shared by all parties `[BS §10.4]`.

### Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]]: Import $(k, T_P)$ — the shared key and the transcript.
> - $\alpha, \beta \in \mathbb Z_q$: the secret exponents of Alice and Bob.
> - $u = g^\alpha$, $v = g^\beta$: the values they send. $w$: the shared secret.

### Algorithms

> [!scheme] Protocol `[BS §10.4]`
> | | Alice | | Bob |
> | --- | --- | --- | --- |
> | 1 | $\alpha \xleftarrow{\$} \mathbb Z_q$<br>$u \leftarrow g^\alpha$ | $\xrightarrow{\ u\ }$ | |
> | 2 | | $\xleftarrow{\ v\ }$ | $\beta \xleftarrow{\$} \mathbb Z_q$<br>$v \leftarrow g^\beta$ |
> | 3 | $w \leftarrow v^\alpha$ | | $w \leftarrow u^\beta$ |
>
> The transcript is $T_P = (u, v)$ and the shared key is $k = w$. The two messages do not depend on each other and can be sent in either order. `[BS §10.4]` `[Gal12 §20.2.1]`

> [!remark] The shape behind it `[BS §10.4]`
> Alice sends $E(\alpha)$ for a random secret $\alpha$, Bob sends $E(\beta)$, and both compute $F(\alpha, \beta)$, where
> 1. $E$ is easy to compute;
> 2. given $\alpha$ and $E(\beta)$, $F(\alpha, \beta)$ is easy to compute;
> 3. given $E(\alpha)$ and $\beta$, $F(\alpha, \beta)$ is easy to compute;
> 4. given $E(\alpha)$ and $E(\beta)$, $F(\alpha, \beta)$ is hard to compute.
>
> Diffie–Hellman takes $E(\alpha) = g^\alpha$ and $F(\alpha, \beta) = g^{\alpha\beta}$; requirement 4 is then the [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|CDH assumption]].

> [!remark] Notation in the literature
> | source | form | differences |
> | --- | --- | --- |
> | `[BS §10.4]` | $u = g^\alpha$, $v = g^\beta$, $w = g^{\alpha\beta}$ | as above |
> | `[Gal12 §20.2.1]` | $c_1 = g^a$, $c_2 = g^b$, $K = g^{ab}$ | $0 < a, b < r$, the group order written $r$ |
> | `[CK01 §4.1]` (2DH) | $\alpha = g^x$, $\beta = g^y$, $\gamma = g^{xy}$ | messages carry the sender's identity and a session id $s$; each party erases its exponent after computing $\gamma$ |
> | `[DH76 §III]` | $Y_i = \alpha^{X_i} \bmod q$, $K_{ij} = \alpha^{X_i X_j} \bmod q$ | $\alpha$ a primitive element of $\mathrm{GF}(q)$, $q$ prime; static values in a public file — see [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange#Original public-key distribution\|#Original public-key distribution]] |

## Property

### Correctness

> [!property] $\mathsf{DH}$ Correctness
> $$v^\alpha = g^{\alpha\beta},$$
> $$u^\beta = g^{\alpha\beta},$$
> so both parties output the same $w$. `[BS §10.4]`

## Security

### Against an eavesdropper

> [!security] Session-key security with authenticated links `[CK01 Thm 2]`
> If the [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|DDH assumption]] holds in $\mathbb G$, the two-move protocol 2DH is SK-secure in the authenticated-links model, where the adversary schedules and reads every message but cannot change or inject any ([[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange#SK-security\|Authenticated Key Exchange#SK-security]]).

> [!remark] The original argument
> `[DH76 §III]` gives no proof: computing $K_{ij}$ from $Y_i, Y_j$ would follow from computing logarithms in $\mathrm{GF}(q)$, and the authors see no other way. With $q$ near $2^b$, the users need at most $2b$ multiplications while the best logarithm algorithm then known needs about $q^{1/2} = 2^{b/2}$ operations: for $b = 200$, about $400$ against $2^{100}$.

> [!question]
> Suppose that Eve has an algorithm that efficiently solves the [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|Diffie-Hellman problem]], can she use it to also efficiently solve the [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|discrete logarithm problem]]? (The other direction is immediate; `[Gal12 Lemma 20.2.5]` records $\mathrm{DDH} \leq_R \mathrm{CDH} \leq_R \mathrm{DLP}$.)

## Cryptanalysis

> [!attack] Man in the middle `[Gal12 §20.5]` `[Cia24]`
> The protocol is not secure against an active adversary: an adversary who intercepts $u$ and $v$ and runs the protocol separately with each party ends with two keys, one shared with Alice and one with Bob, and neither party can detect it. The message flow is in [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack#Against Diffie–Hellman\|Man-in-the-Middle Attack#Against Diffie–Hellman]]. Security above is proved only with authenticated links.

> [!remark] Signing the values is not enough
> `[Gal12 §20.5]` suggests that each party sign its value, given authentic copies of the peers' public keys, and adds that this does not prevent all attacks. The identity-misbinding attack on signed DH is in [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack#Identity misbinding\|Man-in-the-Middle Attack#Identity misbinding]]; [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Sign-and-MAC Key Exchange\|SIGMA]] is a design that resists it.

## Variant

### Original public-key distribution

> [!definition] Parameters
> - $q$: a large prime. $\alpha$: a primitive element of $\mathrm{GF}(q)$.
> - $X_i \in \{1, 2, \dots, q - 1\}$: the secret of user $i$. $Y_i$: its public value.

> [!scheme] Public key distribution with a public file `[DH76 §III]`
> - **Registration** — each user $i$ chooses $X_i$ uniformly and places
>     $$Y_i = \alpha^{X_i} \bmod q$$
>     in a public file, with its name and address; $X_i$ stays secret.
> - **Key** — users $i$ and $j$ use
>     $$K_{ij} = \alpha^{X_i X_j} \bmod q.$$
>     User $i$ fetches $Y_j$ from the file and computes $Y_j^{X_i} \bmod q$; user $j$ computes $Y_i^{X_j} \bmod q$.

> [!remark] Authenticated by the file, and static
> - The public file "must be protected from unauthorized modification"; it needs no read protection, and since it changes rarely, strong write protection is practical `[DH76 §III]`. So the original is authenticated by its directory: a man in the middle must change an entry of the file, not a message.
> - $K_{ij}$ is the same for every conversation between $i$ and $j$; the exchange of fresh $g^\alpha, g^\beta$ per session in [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange#Algorithms\|#Algorithms]] is what later protocols use.

### Elliptic-curve Diffie–Hellman

> [!definition] Parameters
> - $E$: an elliptic curve over $\mathbb F_p$ ([[knowledge/math/algebra/structures/elliptic curve/Elliptic Curves over Finite Fields\|Elliptic Curves over Finite Fields]]). $P \in E(\mathbb F_p)$: a public point of prime order.
> - $n_A, n_B$: the secret integers of Alice and Bob.

> [!scheme] ECDH
> The protocol of [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange#Algorithms\|#Algorithms]] in the group generated by $P$, written additively `[Gal12 §20.1, §20.2.1]`:
> 
> | | Alice | | Bob |
> | --- | --- | --- | --- |
> | 1 | $Q_A \leftarrow n_A P$ | $\xrightarrow{\ Q_A\ }$ | |
> | 2 | | $\xleftarrow{\ Q_B\ }$ | $Q_B \leftarrow n_B P$ |
> | 3 | $K \leftarrow n_A Q_B$ | | $K \leftarrow n_B Q_A$ |
>
> Both obtain $K = n_A n_B P$. Its eavesdropper problem is the elliptic-curve Diffie–Hellman problem: compute $n_1 n_2 P$ from $n_1 P$ and $n_2 P$, the computational Diffie–Hellman problem `[Gal12 Def 20.2.1]` in this group.


### Tripartite Diffie–Hellman

> [!definition] Parameters
> - $E / \mathbb F_q$: an elliptic curve. $P \in E(\mathbb F_q)$: a point of prime order $\ell$.
> - $\phi$: an $\ell$-distortion map for $P$; $\hat e_\ell$: the modified pairing it defines ([[knowledge/math/algebra/structures/elliptic curve/Bilinear Pairings\|Bilinear Pairings]]).
> - $n_A, n_B, n_C$: the secrets of Alice, Bob and Carl.

> [!scheme] Joux's one-round tripartite key exchange `[HPS]`
> - Each party publishes one point:
>     - Alice: $Q_A = n_A P$;
>     - Bob: $Q_B = n_B P$;
>     - Carl: $Q_C = n_C P$.
> - Each computes the key from the other two points:
>     - Alice: $K = \hat e_\ell(Q_B, Q_C)^{n_A}$;
>     - Bob: $K = \hat e_\ell(Q_A, Q_C)^{n_B}$;
>     - Carl: $K = \hat e_\ell(Q_A, Q_B)^{n_C}$.
> - All three equal $\hat e_\ell(P, P)^{n_A n_B n_C}$, by bilinearity.
>
> ⚠️ CLAUDE – verify: kept from the presentation of `[HPS]`, which I could not open, and from Joux's ANTS 2000 paper, which I could not reach.

> [!remark] What breaks it
> If Eve solves the [[knowledge/complexity/problem/group/Elliptic Curve DLP\|ECDLP]], she recovers $n_A$, $n_B$ or $n_C$ and the key. Since $\hat e_\ell$ maps into $\mathbb F_q^*$, a discrete logarithm in the order-$\ell$ subgroup of $\mathbb F_q^*$ ([[knowledge/complexity/problem/group/Discrete Logarithm Problem\|DLP]]) also suffices.

## Related

### Constructions
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Sign-and-MAC Key Exchange\|SIGMA]] — the exchange of [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange#Algorithms\|#Algorithms]], with each value signed and each identity MACed under a key derived from $g^{xy}$
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key-Exchange Authenticator\|Key-Exchange Authenticator]] — applied to 2DH with signatures, it gives SIG-DH, secure against active adversaries

### Siblings
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Merkle Puzzles\|Merkle Puzzles]] — the other public key distribution system of the 1970s, with only a quadratic gap

### Prerequisites
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]] — the primitive
- [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|Discrete-Logarithm Assumption]], [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|Computational Diffie-Hellman Assumption]], [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|Decisional Diffie-Hellman Assumption]] — the assumptions
- [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|Man-in-the-Middle Attack]] — what it does not resist
