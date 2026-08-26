---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/digital-signatures/schemes/dilithium/","dg-note-properties":{}}
---

Reference: 
- https://eprint.iacr.org/2017/633
## Scheme

> [!scheme] Dilithium Signature
> Reference Name: $\text{Dilithium}$
> 
> ---
> ### Parameters
> - $q$: Modulus.
> - $d$: Rounding precision.
> - $\tau$: Weight of challenge polynomial $c$.
> - $\gamma_1$: Masking bound (how large the random masking noise is).
> - $\gamma_2$: Decomposition bound (where the boundaries between high bits lie)
> - $k, \ell$: Matrix dimensions.
> - $\eta$: Secret coefficient size.
> - $\beta$: Rejection threshold.
> - $\omega$: Maximum hint weight.
> - $R_q$: $\mathbb Z_q[X] / (X^n + 1)$
> - $S_\eta$: Set of small polynomials with coefficient less than $\eta$.
> 
> ---
> ### Building Block
> - $c \leftarrow \text{SampleInBall}()$: Cryptographic hash function that hashed onto $B_{60}$.
> 	1. Initialize $c = c_0 c_1 \dots c_{255} = 00 \dots 0$
> 	2. For $i = 196$ to 255: 
> 		1. $j \leftarrow \{0, 1, \dots, i\}, s \leftarrow \{0, 1\}$.
> 		2. $c_i = c_j, c_j = (-1)^s$
> 	3. Return $c$.
> - $\textbf{A} \leftarrow \text{ExpandA}(\rho)$: Maps a uniform seed $\rho \in \{0, 1\}^{256}$ to a matrix $\textbf{A} \in R_q^{k \times l}$ in CRT representation.
> - $y \leftarrow \text{ExpandMask}(K, \mu, \kappa)$: Deterministically generating the randomness of the signature scheme:
> 	- $K$: Secret signing seed.
> 	- $\mu$: Hash of the message.
> 	- $\kappa$: Counter/Nonce.
> 	1. Output $y \in S_{\gamma_1 - 1}^l$
> - $(r_0, r_1) \leftarrow \text{Decompose}_q(r, \alpha)$: Split $r = r_1 \alpha + r_0$ where $-\frac{\alpha}{2} < r_0 \leq \frac{\alpha}{2}$ and also 
> 	- $r_1 \leftarrow \text{HighBits}_q(r, \alpha)$.
> 	- $r_0 \leftarrow \text{LowBits}_q(r, \alpha)$.
> - $h = \{0, 1\} \leftarrow \text{MakeHint}_q(z, r, \alpha)$: Whether adding a small correction $z$ changes the high bits:
> 	1. Returns $h = (\text{HighBits}(r) \neq \text{HighBits}(r + z))$.
> - $\text{UseHint}_q(h, r, \alpha)$:
> 	1. $m = (q - 1) / \alpha$
> 	2. $(r_1, r_0) = \text{Decompose}_q(r, \alpha)$
> 	3. If $h = 1$ and $r_0 > 0$ return $(r_1 + 1) \mod m$
> 	4. If $h = 1$ and $r_0 \leq 0$ return $(r_1 - 1) \mod m$
> 	5. Returns $r_1$
> - $\{0, 1\}^{384} \leftarrow \text{CRH}(m)$: [[knowledge/cryptography/special functions/hash functions/Hash Functions#Collision Resistance\|Collision Resistance Hash Function]] 
> - $(r_1, r_0) \leftarrow \text{Power2Round}_q(r, d)$: Break up an element $r = r_1 \cdot 2^d + r_0$
> 	1. $r = r \bmod q$
> 	2. $r_0 = r \bmod^{\pm} 2^d$
> 	3. Return $((r - r_0) / 2^d, r_0)$
> 
> ---
> ### Algorithms
> - $(pk, sk) \leftarrow \text{Gen}()$:
> 	1. $\rho \leftarrow \{0, 1\}^{256}, K \leftarrow \{0, 1\}^{256}$
> 	2. $(s_1, s_2) \leftarrow S_\eta^\ell \times S_\eta^k$
> 	3. $A \in R_q^{k \times \ell} = \text{ExpandA}(\rho)$
> 	4. $t = As_1 + s_2$
> 	5. $(t_1, t_0) = \text{Power2Round}_q(t, d)$
> 	6. $tr \in \{0, 1\}^{384} = \text{CRH}(\rho || t_1)$
> 	7. Return $(pk = (\rho, t_1), sk = (\rho, K, tr, s_1, s_2, t_0))$
> - $\sigma \leftarrow \text{Sign}(sk = (\rho, K, tr, s_1, s_2, t_0), M)$:
> 	1. $A \in R_q^{k \times \ell} = \text{ExpandA}(\rho)$
> 	2. $\mu \in \{0, 1\}^{384} = \text{CRH}(tr || M)$
> 	3. $\kappa = 0, (z, h) = \perp$
> 	4. While $(z, h) = \perp$ do
> 		1. $y \in S_{\gamma_1 - 1}^\ell = \text{ExpandMask}(K, \mu, \kappa)$
> 		2. $w = Ay$
> 		3. $w_1 = \text{HighBits}_q(w, 2\gamma_2)$
> 		4. $c \in B_{60} = H(\mu || w_1)$
> 		5. $z = y + c s_1$
> 		6. $(r_1, r_0) = \text{Decompose}_q(w - c s_2, 2 \gamma_2)$
> 		7. Branch:
> 			- If $||z||_\infty \geq \gamma_1 - \beta$ or $||r_0||_\infty \geq \gamma_2 - \beta$ or $r_1 \neq w_1$, then $(z, h) = \perp$
> 			- Else
> 				1. $h = \text{MakeHint}_q(-c t_0, w - c s_2 + c t_0, 2 \gamma_2)$
> 				2. If $||c t_0||_\infty \geq \gamma_2$ or the number of 1's in $h$ is greater than $\omega$, then $(z, h) = \perp$.
> 		8. $\kappa = \kappa + 1$
> 	5. Returns $\sigma = (z, h, c)$.
> - $\text{Verify}(pk = (\rho, t_1), M, \sigma = (z, h, c))$:
> 	1. $A \in R_q^{k \times \ell} = \text{ExpandA}(\rho)$
> 	2. $\mu \in \{0, 1\}^{384} = \text{CRH}(\text{CRH}(\rho || t_1) || M)$
> 	3. $w_1' = \text{UseHint}_q(h, Az - c t_1 \cdot 2^d, 2 \gamma_2)$
> 	4. Returns and of three check.
> 		1. $||z||_\infty < \gamma_1 - \beta$  
> 		2. $c = H(\mu || w_1')$  
> 		3. $\text{Number of 1's in } h \text{ is} \leq \omega$.

> [!lemma]
> Suppose that $q$ and $\alpha$ are positive integers satisfying $q > 2 \alpha, q \equiv 1 \pmod \alpha$ and $\alpha$ even. Let $r$ and $z$ be vectors of elements in $R_q$ where $||z||_{\infty} \leq \alpha / 2$, and let $h, h'$ be vectors of bits. Then the $\text{HighBits}_q, \text{MakeHint}_q$, and $\text{UseHint}_q$ algorithms satisfy the following properties:
> 1. $\text{UseHint}_q(\text{MakeHint}_q(z, r, \alpha), r, \alpha) = \text{HighBits}_q(r + z, \alpha)$.
> 2. Let $v_1 = \text{UseHint}_q(h, r, \alpha)$. Then $||r - v_1 \cdot \alpha||_\infty \leq \alpha + 1$. Furthermore, if the number of 1's in $h$ is $\omega$, then all except at most $\omega$ coefficients of $r - v_1 \cdot \alpha$ will have magnitude at most $\alpha / 2$ after centered reduction modulo $q$.
> 3. For any $h, h'$, if $\text{UseHint}_q(h, r, \alpha) = \text{UseHint}_q(h', r, \alpha)$, then $h = h'$.

> [!lemma]
> If $||s||_{\infty} \leq \beta$ and $||\text{LowBits}_q(r, \alpha)||_\infty < \alpha / 2 - \beta$, then $$\text{HighBits}_q(r, \alpha) = \text{HighBits}_q(r + s, \alpha).$$ 

