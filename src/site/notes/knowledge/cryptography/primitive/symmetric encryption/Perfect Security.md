---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/symmetric-encryption/perfect-security/","dg-note-properties":{}}
---

## Definition

> [!definition] Perfect Security
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. Consider a probabilistic experiment in which the random variable $K$ is uniformly distributed over $\mathcal K$. If for all $m_0, m_1 \in \mathcal M$ and all $c \in \mathcal C$: $$P[E(K, m_0) = c] = P[E(K, m_1) = c],$$ then $\mathcal E$ is **perfectly secure**.

## Equivalent Characterizations

> [!theorem] Counting Form
> Let $\mathcal E = (E, D)$ be a Shannon cipher defined over $(\mathcal K, \mathcal M, \mathcal C)$. The following are equivalent:
> 1. $\mathcal E$ is perfectly secure.
> 2. For every $c \in \mathcal C$, there exists an integer $N_c$ (possibly depending on $c$) such that for all $m \in \mathcal M$: $$|\{k \in \mathcal K : E(k, m) = c\}| = N_c.$$
> 3. If $K$ is uniformly distributed over $\mathcal K$, then each of the random variables $E(K, m)$, for $m \in \mathcal M$, has the same distribution.

> [!theorem] Predicate Form
> Consider a probabilistic experiment in which $K$ is uniformly distributed over $\mathcal K$. Then $\mathcal E$ is perfectly secure iff for every predicate $\phi$ on $\mathcal C$, and for all $m_0, m_1 \in \mathcal M$: $$P[\phi(E(K, m_0))] = P[\phi(E(K, m_1))].$$

> [!theorem] Independence Form
> Consider a random experiment in which $K$ and $M$ are random variables such that $K$ is uniform over $\mathcal K$, $M$ is distributed over $\mathcal M$, and $K \perp M$. Let $C = E(K, M)$. Then:
> - If $\mathcal E$ is perfectly secure, then $C$ and $M$ are independent.
> - Conversely, if $C$ and $M$ are independent and each message in $\mathcal M$ occurs with nonzero probability, then $\mathcal E$ is perfectly secure.

## Bounds

See [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Perfect Security\|Symmetric Key Encryption#Perfect Security]] for Shannon's Theorem ($|\mathcal K| \geq |\mathcal M|$) and its generalization to unbounded semantic-security adversaries.

## Case Study

The [[knowledge/cryptography/primitive/symmetric encryption/classical/One-time Pad\|One-time Pad]] is the canonical perfectly secure cipher, meeting Shannon's bound with equality.
