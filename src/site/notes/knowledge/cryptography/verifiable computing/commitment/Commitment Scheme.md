---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/commitment-scheme/","dg-note-properties":{}}
---

Reference:
- https://homepages.cwi.nl/~schaffne/courses/crypto/2014/papers/ComZK08.pdf

## Intuition

> [!example] Coin Flipping by Telephone
> Suppose Alice and Bob are getting a divorce but they can not even stand facing each other, so they have to discuss over the phone how to split the furniture, the kids, etc. Since they can not agree who get which, they decide to flip a coin. To make the game fair, we can use a simple protocol:
> 1. Alice commits to a random bit $b_A$, and sends the resulting commitment $C$ to Bob.
> 2. Bob chooses a random bit $b_B$ and sends it to Alice.
> 3. Alice opens $C$ to let Bob learn $b_A$, and both parties compute the result, which is $b = b_A \oplus b_B$.

## Syntax

> [!definition] Commitment Scheme
> A **commitment scheme** for a finite message space $\mathcal M$, is a pair of efficient algorithms $\mathcal{CS} = (\mathsf{Com}, \mathsf{Verify})$ where:
> - $(c, o) \xleftarrow{\$} \mathsf{Com}(m)$: Commitment algorithm, where $m \in \mathcal M$ is the message to be committed, $c$ is the commitment string, and $o$ is an opening string.
> - $\{0, 1\} \xleftarrow{\$} \mathsf{Verify}(m, c, o)$: Verification algorithm that output $1$ for $\mathsf{accept}$ or $0$ for $\mathsf{reject}$.

> [!definition] Commitment Phases
> - Commit Phase: Sender runs $(c, o) \xleftarrow{\$} \mathsf{Com}(m)$ and sends $c$.
> - Reveal Phase: Sender sends $(m, o)$; receiver runs $\mathsf{Verify}(m, c, o)$.

## Property

### Correctness

> [!definition] Correctness
> For all $m \in \mathcal M$:
> $$\Pr\!\left[
> \begin{array}{l}
> \text{Verify}(m, c, o) = \text{accept}
> \end{array}
> \; \middle | \; 
> \begin{array}{l}
> (c, o) \leftarrow \text{Com}(m)
> \end{array} \right] = 1$$

## Security

### Binding

> [!definition] Binding
> For any adversary $\mathcal{A}^\mathrm{find}$, we define the binding advantage:
> $$\mathsf{Adv}_{\mathcal{CS}}^\mathrm{Bind}(\mathcal{A}) =  
> \; \Pr\!\left[
> \begin{array}{l}
> m_1 \neq m_2 \\
> c_1 = c_2
> \end{array}
> \; \middle | \; 
> \begin{array}{l}
> (m_1, m_2) \leftarrow \mathcal A^\text{find}() \\
> (c_1, o_1) \leftarrow \text{Com}(m_1) \\
> (c_2, o_2) \leftarrow \text{Com}(m_2)
> \end{array} \right]$$

### Hiding

> [!definition] Hiding
> For any adversary $\mathcal A = (\mathcal A_\text{find}, \mathcal A_\text{guess})$, we define the hiding advantage:
> $$\text{Adv}_{\mathcal C}^{\text{Hide}}(\mathcal A) = 
> \left|\; \Pr\!\left[ b = b' \;\middle |\; 
> \begin{array}{l}
> (m_0, m_1, s) \leftarrow \mathcal A_\text{find}(); \\
> b \xleftarrow{\$} \{0, 1\}; (c^*, o^*) \xleftarrow{\$} \text{Com}(m_b) \\
> b' \leftarrow \mathcal A_\text{guess}(s, c^*)
> \end{array} \right] 
> \;- \frac{1}{2}
> \right|.$$

