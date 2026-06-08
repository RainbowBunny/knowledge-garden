---
{"dg-publish":true,"permalink":"/knowledge-1/cryptography/post-quantum-cryptography/lattice-based/lattice/","dg-note-properties":{}}
---

## Basic Definition


## Lattice Trapdoors

> [!lemma]
> Let $q, n, m$ be positive integers with $q \geq 2$ and $m \geq 6n \log_2 q$.
> There is a PPT algorithm $\text{TrapGen}(q, n, m)$ that with probability $1 - 2^{-\ohm(n)}$ outputs a pair $(A, T) \in \mathbb Z_q^{n \times m} \times \mathbb Z^{m \times m}$ such that $A$ is within $2^{-\ohm(n)}$ statistical distance to uniform in $\mathbb Z_q^{n \times m}$ and $T$ is a basis for $\Lambda^{\perp}_q(A)$.
> There is a PPT algorithm $\text{SamplePre}(A, T, u, \sigma)$, which takes as input the above pair $(A, T)$, a vector $u \in \mathbb Z_q^n$ and a sufficiently large $\sigma = \ohm(\sqrt{n \log q \log m})$ and outputs a vector $e$ from $\mathcal D_{\Lambda^u_q(A), \sigma}$. Further, with probability $2^{-\ohm(n)}$, we have $||e|| \leq \sigma \sqrt{m}$.

