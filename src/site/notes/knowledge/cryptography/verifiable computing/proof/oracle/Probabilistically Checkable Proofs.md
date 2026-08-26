---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/oracle/probabilistically-checkable-proofs/","dg-note-properties":{}}
---

Reference: https://www.di.ens.fr/~nitulesc/files/Survey-SNARKs.pdf
## Basic Definition

> [!definition] Restricted PCP Verifier
> For function $r, q: \mathbb Z^+ \rightarrow \mathbb Z^+$ an $(r, q, a)$-restricted PCP verifier is a probabilistic oracle algorithm $V$ that on input $x \in \{0, 1\}^n$, expects a random string $R \in \{0, 1\}^{r(n)}$ and queries an oracle $\Pi: \mathbb Z^+ \rightarrow \{0, 1\}^{a(n)}$ at most $q(n)$ times and computes a "Boolean verdict" $V^\Pi(x; R) \in \{0, 1\}$.

> [!definition] Probabilistically Checkable Proof
> Let $\mathcal L$ be a language and $q, r: \mathbb N \rightarrow \mathbb N$. A probabilistically checkable proof system $\text{PCP}(r(n), q(n))$ for $\mathcal L$ is a probabilistic polynomial-time oracle machine, called verifier and denoted $\mathcal V$, that satisfies: "Efficiency", "Completeness", "Soundness".

### PCP Theorem

> [!theorem] PCP Theorem
> $$\text{NP} = \text{PCP}(\log n, 1)$$

## Property

### Efficiency

> [!definition] Efficiency
> On input a string $x \in \{0, 1\}^n$, and given a random access to a string $\pi$ called the proof, $\mathcal V$ uses at most $r(n)$ random coins and makes at most $q(n)$ queries to locations of $\pi$. Then it outputs 1 (for "accept") or 0 (for "reject").

### Completeness

> [!definition] Completeness
> For every $x \in \mathcal L$ there exists a proof string $\pi$ such that, on input $x$ and access to oracle $\pi$, $\mathcal V$ always accepts $x$.

## Security

### Soundness

> [!definition] Soundness
> For every $x \notin \mathcal L$ and every proof string $\pi$, on input $x$ and access to oracle $\pi$, $\mathcal V$ rejects $x$ with probability at least 1/2.
