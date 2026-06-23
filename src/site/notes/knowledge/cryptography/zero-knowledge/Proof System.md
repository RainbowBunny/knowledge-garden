---
{"dg-publish":true,"permalink":"/knowledge/cryptography/zero-knowledge/proof-system/","dg-note-properties":{}}
---

## Syntax

> [!definition] Proof System
> A proof system is a protocol consists of two parties $(P, V)$ and a pair of algorithms $(\text{Execute}, \text{Verify})$ that works with a [[NP Relation\|NP Relation]] $R$ and its language 
> $$L_R = \{x \; | \; \exists w : R(x, w) = 1\}$$
> - $\tau \leftarrow \text{Execute}_{P, V}(x, w; r_P, r_V)$: The prover have a [[witness\|witness]] of a **public statement** $x$, this function returns the transcript of the conversation of two parties in which the prover is trying to convince the verifier that $w$ is the witness of $x$ as the verifier $V$ is only guarantee to have $x$.
> - $\{\text{accept}, \text{reject}\} \leftarrow \text{Verify}(x, \tau; r_V)$: Given the public statement $x$ and transcript of the conversation $\tau$, the verifier $V$ can tell whether the claim of prover $P$ is correct.

## Property

### Completeness

> [!definition] Proof System's Completeness
> An honest prover $P$ with a valid witness $w$ for statement $x$ should convince the verifier $V$:
> $$\Pr[\text{Verify}(x, \text{Execute}_{P, V}(x, w)) = \text{accept}] \geq 1 - \varepsilon_c \; \forall (x, w) \in R$$

### Soundness

> [!definition] Proof System's Soundness
> For every cheating prover $P^*$ for statement $x$, we have
> $$\Pr[\text{Verify}(x, \text{Execute}_{P^*, V}(x)) = \text{reject}] \leq \varepsilon_s$$

> [!remark]
> Soundness means you should not be able to prove false statements.

### Knowledge Soundness

> [!definition] Proof System's Knowledge Soundness
> Let $\mathcal O_{P^*}$ be an oracle 

> [!remark]
> Knowledge Soundness means if you prove a statement, you must actually know a witness

## Security

### Zero Knowledge

> [!definition] Zero Knowledge Proof System
> A proof system is zero knowledge if there exist a [[simulator\|simulator]] $\text{Sim}$ and let $\text{View}_V$ be a random variable from the space of available information that given to verifier $V$ and we should have its distribution and the simulating distribution computationally indistinguishable:
> $$\text{View}_V(x, r_V, \text{Execute}_{P, V}(x, w)) \sim \text{Sim}(x)$$

> [!definition] Honest Verifier Zero Knowledge
> Restrict verifier $V$ of the above definition to be honest.


## Overview

> [!proposition]
> A good zero-knowledge proof showing that a quantity $y$ has some property $\mathcal P$ should satisfy the following two conditions:
> - **Completeness**: If $y$ does have property $\mathcal P$, then Victor should always accept Peggy's responses as being valid.
> - **Soundness**: If $y$ does not have property $\mathcal P$, then there should be only a very small probability that Victor accepts all of Peggy's responses as begin valid.

> [!example]
> Peggy chooses two large primes $p$ and $q$ and publishes their product $N$. Peggy's task is to prove to Victor that a certain number $y$ is a square modulo $N$. Peggy's task is to prove to Victor that a certain number $y$ is a square modulo $N$ without revealing to Victor any information that would help him to prove to other people that $y$ is a square modulo $N$. We note that since Peggy knows how to factor $N$, if $y$ is a square modulo $N$, then she can find a square root for $y$, say $x$ satisfying $$x^2 \equiv y \pmod N.$$ In each round, Peggy and Victor perform the following steps:
> 1. Peggy chooses a random number $r$ modulo $N$. She computes and sends to Victor the number $$s \equiv r^2 \pmod N.$$
> 2. Victor randomly chooses a value $\beta \in \{0, 1\}$ and sends $\beta$ to Peggy.
> 3. Peggy computes and sends to Victor the number $$z \equiv \begin{cases}r \pmod N &\text{if } \beta = 0. \\ xr \pmod N \; &\text{if } \beta = 1.\end{cases}$$
> 4. Victor computes $z^2 \pmod N$ and checks that $$z^2 \equiv \begin{cases}s \pmod N &\text{if } \beta = 0. \\ ys \pmod N \; &\text{if } \beta = 1.\end{cases}$$
> If this is true, Victor accepts Peggy's response; otherwise, he rejects it.

## Term Reference

| Term                                              | Reference                                                                                |                   |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------- | ----------------- |
| Attack Game 20.1 (Soundness)                      | [[knowledge/cryptography/zero-knowledge/Interactive Zero Knowledge#Soundness\|soundness]]                                      | $\text{Sndadv}$   |
| Attack Game 20.2 (Non-Interactive Soundness)      | [[knowledge/cryptography/zero-knowledge/Non-Interactive Zero Knowledge#Non-Interactive Soundness\|non-interactive soundness]]  | $\text{niSndadv}$ |
| Attack Game 20.3 (Non-Interactive Zero Knowledge) | [[knowledge/cryptography/zero-knowledge/Non-Interactive Zero Knowledge#Non-Interactive Zero Knowledge\|non-interactive zero knowledge]] | $\text{niZKadv}$  |

## Preliminaries

### Languages of True Statements

> [!definition] Languages of True Statements
> Let $\mathcal R \subseteq \mathcal X \times \mathcal Y$ be an effective relation. We say a statement $y \in \mathcal Y$ is a **true statement** if $(x, y) \in \mathcal R$ for some $x \in \mathcal X$; otherwise, we say that $y \in \mathcal Y$ is a **false statement**. We define $L_{\mathcal R}$, which is called **language defined by** $\mathcal R$, to be the set of all true statements; that is, $L_{\mathcal R} = \{y \in \mathcal Y: (x, y) \in \mathcal R \text{ for some } x \in \mathcal X\}$.
