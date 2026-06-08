---
{"dg-publish":true,"permalink":"/academic/knowledge/cryptography/public-key-encryption/schemes/kyber-pke/","dg-note-properties":{}}
---

Link: https://eprint.iacr.org/2017/634.pdf
## Scheme

> [!scheme] Kyber PKE
> Reference Name: $\text{Kyber.PKE}$
> 
> ---
> ### Parameters
> - $\eta$: Noise parameter.
> - $\beta_\eta$: Centered binomial distribution with parameter $\eta$.
> - $k$: Module rank, the dimension of vectors and matrices over $R_q$.
> - $d_t$: Public-key compression parameter for each coefficient $t$.
> - $d_u$: Ciphertext compression parameter for $u$.
> - $d_v$: Ciphertext compression parameter for $v$.
> 
> ---
> ### Building Block
> - $\text{Sam}$: Extendable output function.
> - $\text{Compress}_q(x, d)$: Takes an element $x \in \mathbb Z_q$ and outputs an integer in $\{0, \dots, 2^d - 1\}$, where $d < \lceil \log_2(q) \rceil$:
> 	1. Output $\lceil (2^d / q) \cdot x \rfloor \mod 2^d$.
> - $\text{Decompress}_q(x, d)$: Output an element $x'$ close to $x$ that satisfies $|x' - x \mod^{\pm} q| \leq B_q = \lceil \frac{q}{2^{d + 1}} \rfloor$.
> 	1. Output $\lceil (q / 2^d) \cdot x \rfloor$
> 
> ---
> ### Algorithms
> - $(pk, sk) \leftarrow \text{KeyGen}()$:
> 	1. $\rho, \sigma \leftarrow \{0, 1\}^{256}$
> 	2. $A \sim R_q^{k \times k} = \text{Sam}(\rho)$
> 	3. $(s, e) \sim \beta_\eta^k \times \beta_\eta^k = \text{Sam}(\sigma)$
> 	4. $t = \text{Compress}_q(As + e, d_t)$
> 	5. Return $(pk = (t, \rho), sk = s)$
> - $c \leftarrow \text{Enc}(pk = (t, \rho), m \in \mathcal M)$: 
> 	1. $r \leftarrow \{0, 1\}^{256}$
> 	2. $t = \text{Decompress}_q(t, d_t)$
> 	3. $A \sim R_q^{k \times k} = \text{Sam}(\rho)$
> 	4. $(r, e_1, e_2) \sim \beta_\eta^k \times \beta_\eta^k \times \beta_\eta = \text{Sam}(r)$
> 	5. $u = \text{Compress}_q(A^T r + e_1, d_u)$
> 	6. $v = \text{Compress}_q(t^T r + e_2 + \lceil \frac{q}{2} \rfloor \cdot m, d_v)$
> 	7. Return $c = (u, v)$.
> - $m \leftarrow \text{Dec}(sk = s, c = (u, v))$:
> 	1. $u = \text{Decompress}_q(u, d_u)$
> 	2. $v = \text{Decompress}_q(v, d_v)$
> 	3. Return $\text{Compress}_q(v - s^T u, 1)$

## Property

### Correctness

> [!property] $\text{Kyber.PKE}$ Correctness
> Let $k$ be a positive integer parameter. Let $s, e, r, e_1, e_2$ be random variables that have the same distribution. Also, let $c_t \leftarrow \psi_{d_t}^k, c_u \leftarrow \psi_{d_u}^k, c_v \leftarrow \psi_{d_v}$ be distributed according to the distribution $\psi$ defined as follows:
> Let $\psi_d^k$ be the following distribution over $R$:
> 1. Choose uniformly-random $y \leftarrow R^k$.
> 2. Return $(y-\text{Decompress}_q(\text{Compress}_q(y, d), d)) \mod^{\pm} q$.
> 
> Denote $$\delta = \Pr[||e^T r + e_2 + c_v - s^T e_1 + c_t^T r - s^T c_u||_\infty \geq \lceil q / 4 \rfloor]$$
> Then, $\text{Kyber.PKE}$ is $(1 - \delta)$-correct.

## Security

### Indistinguishability under Chosen-Plaintext Attacks

> [!security]
> For any [[academic/knowledge/cryptography/public-key encryption/Public Key Encryption#Indistinguishability under Chosen-Plaintext Attacks\|CPA adversary]] $\mathcal A$, there exists an [[academic/knowledge/cryptography/assumptions/lattice-based/LWE/Module Learning With Error#Assumption\|MLWE adversary]] $\mathcal B$ such that: $$\text{Adv}_{Kyber.PKE}^{\text{cpa}}(\mathcal A) \leq 2 \cdot \text{Adv}_{k + 1, k, \eta}^{\text{mlwe}}(\mathcal B).$$

