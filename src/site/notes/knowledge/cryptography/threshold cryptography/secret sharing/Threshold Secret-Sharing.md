---
{"dg-publish":true,"permalink":"/knowledge/cryptography/threshold-cryptography/secret-sharing/threshold-secret-sharing/","dg-note-properties":{}}
---

## Syntax

> [!definition] Threshold Secret Sharing Scheme
> A **$t$-out-of-$n$ threshold secret-sharing scheme** $\text{TSS} = (\text{Share}, \text{Reconstruct})$ is a pair of efficient algorithms with a message space $\mathcal M$ and **threshold** $t$:
> - $(s_1, \dots, s_n) \leftarrow \text{Shares}(m)$: The randomized algorithm $\text{Shares}$ that takes a **message** $m \in \mathcal M$ as input, and outputs a sequence $(s_1, \dots, s_n)$ of **shares**.
> - $m \leftarrow \text{Reconstruct}(s_{i_1}, \dots, s_{i_t}, \dots, s_{i_m})$: The deterministic algorithm that takes a collection of $t$ or more shares as input, and outputs a message.

> [!definition] Authorized Set
> Number the users as $\{1, \dots, n\}$, with user $i$ receiving share $s_i$. Let $U \subseteq \{1, \dots, n\}$ be a subset of users. Then $\{s_i \; | \; i \in U\}$ refers to the set of shares belonging to users $U$. If $|U| \geq t$, we say that $U$ is **authorized**; otherwise it is **unauthorized**. The goal of secret sharing is for all authorized sets of users/shares to be able to reconstruct the secret, while all unauthorized sets learn nothing.

## Property

### Correctness

> [!definition] TSS Correctness
> A $t$-out-of-$n$ TSS satisfies **correctness** if, for all authorized sets $U \subseteq \{1, \dots, n\}$ (i.e., $|U| \geq t$) and for all $(s_1, \dots, s_n) \leftarrow \text{Share}(m)$, we have
> $$\text{Reconstruct}(\{s_i \; | \; i \in U\}) = m$$

## Security

### Privacy

> [!definition] TSS Privacy Advantage
> For any adversary $\mathcal A = (\mathcal A_{\text{find}}, \mathcal A_{\text{guess}})$, we define the privacy advantage:
> $$\text{Adv}_\text{TSS}^\text{priv}(\mathcal A) = 
> \left|\; \Pr\!\left[ b = b' \;\middle |\; 
> \begin{array}{l}
> (m_0, m_1, U, s) \leftarrow \mathcal A_\text{find}(); \\
> b \xleftarrow{\$} \{0, 1\}; \\
> (s_1, \dots, s_n) \leftarrow \text{Share}(m_b); \\
> b' \leftarrow \mathcal A_\text{guess}(s, \{s_i \; | \; i \in U\})
> \end{array} \right] 
> \;- \frac{1}{2}
> \right|.$$

