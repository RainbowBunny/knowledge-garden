---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/scheme/el-gamal-signature/","dg-note-properties":{"aliases":["ElGamal Signature Scheme","ElGamal Digital Signature"]}}
---

Reference:
- `[HAC]` — A. J. Menezes, P. C. van Oorschot, S. A. Vanstone, _Handbook of Applied Cryptography_, CRC Press, 1996, §11.5.2: Algorithms 11.63 and 11.64, Notes 11.66 and 11.67: https://cacr.uwaterloo.ca/hac/about/chap11.pdf
- `[PS00]` — D. Pointcheval, J. Stern, _Security Arguments for Digital Signatures and Blind Signatures_, Journal of Cryptology 13(3), 361–396, 2000: §3.3 (Theorem 5; the modified scheme of §3.3.2, Definition 7, Theorems 6 and 7): https://www.di.ens.fr/~pointche/Documents/Papers/2000_joc.pdf
- `[ElG85]` — T. ElGamal, _A Public Key Cryptosystem and a Signature Scheme Based on Discrete Logarithms_, IEEE Transactions on Information Theory 31, 469–472, 1985 — the original; not read.

## Scheme

Reference Name: $\mathsf{ElGamalSig}$
Instantiates:: [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]

> [!scheme] Setting
> - $\mathbb Z_p^*$, for a large prime $p$, with a generator $g$: a [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|Cyclic Group]] of order $p - 1$.
> - Exponents live in $\mathbb Z_{p-1}$, so the signing equation is solved modulo $p - 1$.
>
> `[HAC Alg 11.63]`

> [!definition] Parameters
> - $\lambda$: the security parameter.
> - $(\mathrm{pk}, \mathrm{sk})$: a key pair.
> - $m \in \{0, 1\}^*$: a message.
> - $\sigma = (r, s) \in \mathbb Z_p^* \times \mathbb Z_{p-1}$: a signature.
> - $p$: the prime.
> - $g$: the generator.
> - $a \in \{1, \dots, p - 2\}$: the secret exponent.
> - $y = g^a \bmod p$: the public element.
> - $k \in \{1, \dots, p - 2\}$ with $\gcd(k, p - 1) = 1$: the per-signature secret, fresh for every message.

> [!definition] Building Blocks
> - $H$: a [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]] from messages to $\mathbb Z_{p-1}$.

> [!scheme] ElGamal Signature
> - $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda)$: (Randomized) Key-generation algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: a public key $\mathrm{pk} = (p, g, y)$ and a secret key $\mathrm{sk} = (p, g, a)$.
>     - **Steps**:
>         1. Generates a large random prime $p$ and a generator $g$ of $\mathbb Z_p^*$.
>         2. Samples $a \xleftarrow{\$} \{1, \dots, p - 2\}$.
>         3. Computes $y = g^a \bmod p$.
>         4. Returns $(\mathrm{pk}, \mathrm{sk})$.
> - $\sigma \leftarrow \mathsf{Sign}(\mathrm{sk}, m)$: (Randomized) Signing algorithm.
>     - **Input**: a secret key $\mathrm{sk} = (p, g, a)$ and a message $m$.
>     - **Output**: a signature $\sigma = (r, s) \in \mathbb Z_p^* \times \mathbb Z_{p-1}$.
>     - **Steps**:
>         1. Samples $k \xleftarrow{\$} \{1, \dots, p - 2\}$ with $\gcd(k, p - 1) = 1$.
>         2. Computes $r = g^k \bmod p$.
>         3. Computes $s = k^{-1} \big(H(m) - a r\big) \bmod (p - 1)$.
>         4. Returns $\sigma = (r, s)$.
> - $b \leftarrow \mathsf{Verify}(\mathrm{pk}, m, \sigma)$: (Deterministic) Verification algorithm.
>     - **Input**: a public key $\mathrm{pk} = (p, g, y)$, a message $m$ and a signature $\sigma = (r, s)$.
>     - **Output**: $1$ (accept) or $0$ (reject).
>     - **Steps**:
>         1. Returns $0$ unless $1 \leq r \leq p - 1$.
>         2. Computes $v_1 = y^r r^s \bmod p$ and $v_2 = g^{H(m)} \bmod p$.
>         3. Returns $1$ if $v_1 = v_2$, and $0$ otherwise.
>
> `[HAC Alg 11.63, 11.64]`

> [!remark] Notation in the literature
> | source | form | differences |
> | --- | --- | --- |
> | `[HAC Alg 11.63–11.64]` | $y = \alpha^a$; $r = \alpha^k$, $s = k^{-1}(h(m) - a r)$ | generator $\alpha$, hash $h$; $\mathrm{pk} = (p, \alpha, y)$, $\mathrm{sk} = a$ |
> | `[PS00 §3.3.1]` | $y = g^x$; $m = x r + K s \bmod (p - 1)$ | the original scheme signs $m$ itself, without a hash; secret $x$, per-signature secret $K$ |

## Property

### Correctness

> [!property] $\mathsf{ElGamalSig}$ Correctness `[HAC Alg 11.64]`
> Multiplying the signing equation by $k$ gives $H(m) \equiv a r + k s \pmod{p - 1}$, so
> $$g^{H(m)} \equiv g^{a r + k s} \equiv (g^a)^r (g^k)^s \equiv y^r r^s \pmod p,$$
> and $1 \leq r \leq p - 1$ since $r \in \mathbb Z_p^*$.

## Security

> [!security] What is and is not proved
> - The scheme as above has no security reduction in these sources. Without the hash it is existentially forgeable `[PS00 Thm 5]` — see Cryptanalysis.
> - A modified scheme, hashing $f(m, r)$ in place of $H(m)$, is existentially unforgeable under adaptive chosen-message attack ([[knowledge/cryptography/primitive/digital signatures/Digital Signature#Unforgeability\|Digital Signature#Unforgeability]]) in the [[knowledge/cryptography/assumptions/idealized models/Random Oracle Model\|random oracle model]], if the [[knowledge/complexity/problem/group/Discrete Logarithm Problem\|Discrete Logarithm Problem]] is hard for $\alpha$-hard primes $p$ — those with $p - 1 = qR$, $q$ prime and $R$ polynomially bounded `[PS00 Def 7, Thm 7]`. The reduction goes through the forking lemma and is not tight `[PS00 §3.3]`.

## Cryptanalysis

> [!attack] Reusing $k$ reveals the key `[HAC Note 11.66]`
> Two signatures $(r, s_1)$ on $m_1$ and $(r, s_2)$ on $m_2$ with the same $k$ satisfy
> $$(s_1 - s_2) \, k \equiv H(m_1) - H(m_2) \pmod{p - 1}.$$
> If $s_1 - s_2 \not\equiv 0 \pmod{p - 1}$, this gives $k = (s_1 - s_2)^{-1} \big(H(m_1) - H(m_2)\big) \bmod (p - 1)$, and then $a$, as below.

> [!attack] A known $k$ reveals the key
> The signing equation reads $a r \equiv H(m) - k s \pmod{p - 1}$. If $\gcd(r, p - 1) = 1$, then
> $$a = r^{-1} \big(H(m) - k s\big) \bmod (p - 1);$$
> otherwise it leaves $\gcd(r, p - 1)$ candidates for $a$, each checked against $y = g^a$. So $k$ must stay secret as well as fresh — `[HAC Alg 11.64]` calls it a random *secret* integer.

> [!attack] Without the hash — existential forgery `[HAC Note 11.66]` `[PS00 Thm 5]`
> If $m$ is signed directly, $s = k^{-1}(m - a r) \bmod (p - 1)$. Pick $u, v$ with $\gcd(v, p - 1) = 1$ and set
> $$r = g^u y^v \bmod p, \qquad s = -r v^{-1} \bmod (p - 1);$$
> then $(r, s)$ is a valid signature on $m = s u \bmod (p - 1)$, a message the forger does not choose. Hashing the message blocks this.

> [!attack] Skipping the check $1 \leq r \leq p - 1$ `[HAC Note 11.66]`
> From one valid signature $(r, s)$ on $m$, a forger signs any $m'$: $u = H(m') \, H(m)^{-1} \bmod (p - 1)$, $s' = s u \bmod (p - 1)$, and $r'$ from the Chinese remainder theorem with $r' \equiv r u \pmod{p - 1}$ and $r' \equiv r \pmod p$. Then $y^{r'} r'^{s'} \equiv (y^r r^s)^u \equiv g^{H(m')} \pmod p$. Such an $r'$ is in general larger than $p - 1$, which the check rejects.

> [!attack] Weak generators `[HAC Note 11.67]`
> When $p \equiv 1 \pmod 4$ and $g$ is a generator for which logarithms are easy in a subgroup, a forger can produce signatures with a specially chosen $r$. Taking $g$ to generate a subgroup of $\mathbb Z_p^*$ of prime order avoids it.

## Related

### Siblings
- [[knowledge/cryptography/primitive/digital signatures/Digital Signature Algorithm\|Digital Signature Algorithm]] — `[HAC §11.5]` treats DSA and ElGamal signatures together, as related schemes
- [[knowledge/cryptography/primitive/public-key encryption/scheme/ElGamal Encryption\|ElGamal Encryption]] — the same key pair $(a, g^a)$, used to encrypt

### Prerequisites
- [[knowledge/complexity/problem/group/Discrete Logarithm Problem\|Discrete Logarithm Problem]], [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]], [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]]
