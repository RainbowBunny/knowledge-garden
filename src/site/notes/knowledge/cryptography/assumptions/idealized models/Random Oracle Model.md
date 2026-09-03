---
{"dg-publish":true,"permalink":"/knowledge/cryptography/assumptions/idealized-models/random-oracle-model/","dg-note-properties":{}}
---

Reference: https://snargsbook.org/

## Definition

> [!definition] Random Oracles
> Given a domain $X$ and a range set $Y$, we denote by $\mathcal U(X \rightarrow Y)$ the uniform distribution over all functions of the form $f: X \rightarrow Y$; equivalently, if $f$ is sampled from $\mathcal U(X \rightarrow Y)$, then for every input $x$ it holds that $y = f(x)$ is a uniformly random element in $Y$ (sampled indepedently for each input).
> 
> We denote 
> $$\mathcal U(Y) = \mathcal U(\{0, 1\}^* \rightarrow Y).$$
> 
> And also, we denote the random oracle with (binary) output size $\sigma$
> $$\mathcal U_b(\sigma) = \mathcal U(\{0, 1\}^* \rightarrow \{0, 1\}^\sigma).$$

> [!definition] Random Oracle Model
> The **ROM with (binary) output size** $\sigma \in \mathbb N$ is the model where all parties (honest and malicious) are oracle algorithms and they are each given query access to the same function $f: \{0, 1\}^* \rightarrow \{0, 1\}^\sigma$ sampled from the distribution $\mathcal U_b(\sigma)$.

### Query Encodings

> [!remark] Query Encodings
> As a random oracle $f \in \mathcal U(Y)$ can receive as input any query $x \in \{0, 1\}^*$. Sometimes, we will define $x$ as a tuple assembled from other binary strings.

### Query-answer Traces

> [!definition] Query-Answer Traces
> Sometimes we analyze the *query-answer trace* between an algorithm $A$ and an oracle $f \in \mathcal U(Y)$. We use the notation
> $$b \xleftarrow{\text{tr}} A^f(a)$$
> to denote the fact that $\text{tr}$ is the ordered list of query-answer pairs made/received by the algorithm $A$ on input $a$; note that $\text{tr}$ is a random variable if the algorithm $A$ is probabilistic.

### Query Size

> [!definition] Query Size
> An algorithm $A$ can query the random oracle $f$ at inputs of different size. The **query size** of a query $x$ to $f$ is defined to be $\text{len}(x)$.


## Security Analyses with ROM

### Bounded-Query

> [!definition] Bounded-query Adversaries
> In this setting, we bound the number of queries that the adversary can make to the random oracle, but do *not* bound any of the adversary's other resources (in time, space, randomness, and so on). 
> 
> We use the integer symbol $t \in \mathbb N$ to denote the adversary's query bound. Intuitively, as $t$ grows, so does the ability of a $t$-query adversary to break the security of a given cryptographic protocol.

> [!remark]
> This is sometimes refer to the "pure" ROM where protocols can leverage, and only leverage, the same random function given to everyone.

> [!remark]
> Any result achieved in the setting of bounded-query adversaries directly holds in the setting of bounded-time adversaries (but not vice versa).

### Bounded-Time

> [!definition] Bounded-time Adversaries
> In this setting, we bound the running time of an adversary, and in particular also bound its number of queries to the random oracle. (An adversary can make no more queries than its running time because performing a query consumes one unit of time).

## Lazy Sampling

> [!definition] Lazy Sampling
> Lazily sampling an oracle from $\mathcal U(X \rightarrow Y)$ corresponds to an instance of the following probabilistic stateful algorithm:
> - **Initialization**: Set the internal state $S$ to be an empty mapping.
> - **To answer a query $x \in X$**: If $S$ contains the key $x$ then set $y = S[x]$; otherwise, sample $y \leftarrow Y$, and set $S[x] = y$. Output $y$.

